# Views API

## How Global Custom Text tokens work

{% tabs %}
{% tab title="render\_altered" %}
{% code title="views\_handler\_field.inc" %}
```php
/**
   * Render this field as altered text, from a fieldset set by the user.
   */
  public function render_altered($alter, $tokens) {
    // We trust admins so we allow any tag content. This is important for
    // displays such as XML where we should not mess with tags.
    $value = $alter['text'];
    $value = strtr($value, $tokens);
    // User might already used '%5B' and '%5D' instead of literal [ and ].
    // After token replacements, we need to convert those codes to literal
    // square bracket characters. Otherwise problems like comment #5 and #6 of
    // https://www.drupal.org/node/578772 will happen.
    // We could have used rawurldecode() also, but not sure about the consequences.
    $value = strtr($value, array('%5B' => '[', '%5D' => ']'));

    return $value;
  }
```
{% endcode %}
{% endtab %}

{% tab title="render\_text" %}
{% code title="views\_handler\_field.inc" %}
```php
/**
   * Perform an advanced text render for the item.
   *
   * This is separated out as some fields may render lists, and this allows
   * each item to be handled individually.
   */
  public function render_text($alter) {
    $value = $this->last_render;

    if (!empty($alter['alter_text']) && $alter['text'] !== '') {
      $tokens = $this->get_render_tokens($alter);
      $value = $this->render_altered($alter, $tokens);
    }

    if (!empty($this->options['alter']['trim_whitespace'])) {
      $value = trim($value);
    }

    // Check if there should be no further rewrite for empty values.
    $no_rewrite_for_empty = $this->options['hide_alter_empty'] && $this->is_value_empty($this->original_value, $this->options['empty_zero']);

    // Check whether the value is empty and return nothing, so the field isn't
    // rendered. First check whether the field should be hidden if the
    // value(hide_alter_empty = TRUE) /the rewrite is empty (hide_alter_empty =
    // FALSE). For numeric values you can specify whether "0"/0 should be empty.
    if ((($this->options['hide_empty'] && empty($value))
        || ($alter['phase'] != VIEWS_HANDLER_RENDER_TEXT_PHASE_EMPTY && $no_rewrite_for_empty))
      && $this->is_value_empty($value, $this->options['empty_zero'], FALSE)) {
      return '';
    }
    // Only in empty phase.
    if ($alter['phase'] == VIEWS_HANDLER_RENDER_TEXT_PHASE_EMPTY && $no_rewrite_for_empty) {
      // If we got here then $alter contains the value of "No results text"
      // and so there is nothing left to do.
      return $value;
    }

    if (!empty($alter['strip_tags'])) {
      $value = strip_tags($value, $alter['preserve_tags']);
    }

    $suffix = '';
    if (!empty($alter['trim']) && !empty($alter['max_length'])) {
      $length = strlen($value);
      $value = $this->render_trim_text($alter, $value);
      if ($this->options['alter']['more_link'] && strlen($value) < $length) {
        $tokens = $this->get_render_tokens($alter);
        $more_link_text = $this->options['alter']['more_link_text'] ? $this->options['alter']['more_link_text'] : t('more');
        $more_link_text = strtr(filter_xss_admin($more_link_text), $tokens);
        $more_link_path = $this->options['alter']['more_link_path'];
        $more_link_path = strip_tags(decode_entities(strtr($more_link_path, $tokens)));

        // Take sure that paths which was runned through url() does work as
        // well.
        $base_path = base_path();
        // Checks whether the path starts with the base_path.
        if (strpos($more_link_path, $base_path) === 0) {
          $more_link_path = drupal_substr($more_link_path, drupal_strlen($base_path));
        }

        $more_link = l($more_link_text, $more_link_path, array('attributes' => array('class' => array('views-more-link'))));

        $suffix .= " " . $more_link;
      }
    }

    if (!empty($alter['nl2br'])) {
      $value = nl2br($value);
    }
    $this->last_render_text = $value;

    if (!empty($alter['make_link']) && !empty($alter['path'])) {
      if (!isset($tokens)) {
        $tokens = $this->get_render_tokens($alter);
      }
      $value = $this->render_as_link($alter, $value, $tokens);
    }

    return $value . $suffix;
  }

  /**
   * Render this field as altered text, from a fieldset set by the user.
   */
  public function render_altered($alter, $tokens) {
    // We trust admins so we allow any tag content. This is important for
    // displays such as XML where we should not mess with tags.
    $value = $alter['text'];
    $value = strtr($value, $tokens);
    // User might already used '%5B' and '%5D' instead of literal [ and ].
    // After token replacements, we need to convert those codes to literal
    // square bracket characters. Otherwise problems like comment #5 and #6 of
    // https://www.drupal.org/node/578772 will happen.
    // We could have used rawurldecode() also, but not sure about the consequences.
    $value = strtr($value, array('%5B' => '[', '%5D' => ']'));

    return $value;
  }
```
{% endcode %}
{% endtab %}

{% tab title="get\_render\_tokens" %}
```php
/**
   * Get the 'render' tokens to use for advanced rendering.
   *
   * This runs through all of the fields and arguments that are available and
   * gets their values. This will then be used in one giant str_replace().
   */
  public function get_render_tokens($item) {
    $tokens = array();
    if (!empty($this->view->build_info['substitutions'])) {
      $tokens = $this->view->build_info['substitutions'];
    }
    $count = 0;
    foreach ($this->view->display_handler->get_handlers('argument') as $arg => $handler) {
      $token = '%' . ++$count;
      if (!isset($tokens[$token])) {
        $tokens[$token] = '';
      }

      // Use strip tags as there should never be HTML in the path. However, we
      // need to preserve special characters like " that were removed by
      // check_plain().
      $tokens['!' . $count] = isset($this->view->args[$count - 1]) ? strip_tags(decode_entities($this->view->args[$count - 1])) : '';
    }

    // Get flattened set of tokens for any array depth in $_GET parameters.
    $tokens += $this->get_token_values_recursive($_GET);

    // Now add replacements for our fields.
    foreach ($this->view->display_handler->get_handlers('field') as $field => $handler) {
      if (isset($handler->last_render)) {
        $tokens["[$field]"] = $handler->last_render;
      }
      else {
        $tokens["[$field]"] = '';
      }
      if (!empty($item)) {
        $this->add_self_tokens($tokens, $item);
      }

      // We only use fields up to (and including) this one.
      if ($field == $this->options['id']) {
        break;
      }
    }

    // Store the tokens for the row so we can reference them later if necessary.
    $this->view->style_plugin->render_tokens[$this->view->row_index] = $tokens;
    $this->last_tokens = $tokens;

    return $tokens;
  }
```
{% endtab %}
{% endtabs %}

### get\_render\_tokens example result

```text
(
    [%page] => 1
    [%q] => dev/dc4/dashboard
    [[startDate]] => 09-20-2010
    [[endDate]] => 05-26-2011
    [[firstName]] => DAVID
    [[lastName]] => BRADLEY
    [[email]] => david.bradley@carlsbad.k12.nm.us
    [[students]] => 3
    [[userID]] => 319,180
    [[invoiceID]] => 9,026
    [[start_end_date]] => 09-20-2010<br />
05-26-2011
    [[schoolName]] => ALTA VISTA MIDDLE
    [[educator]] => DAVID BRADLEY<br />
david.bradley@carlsbad.k12.nm.us
    [[student_grade]] => 3
)
```



`$this->view->style_plugin`

![](.gitbook/assets/image%20%2828%29.png)

## Execution order

**Basic execution order:**

1. _**hook\_views\_pre\_view**_
2. _**hook\_views\_pre\_build**_
3. _**hook\_views\_post\_build**_
4. _**hook\_views\_pre\_execute**_
5. _**hook\_views\_post\_execute**_
6. _**hook\_views\_pre\_render**_
7. _**hook\_views\_post\_render**_

**hook\_views\_pre\_view**  
Allows altering a view at the very beginning of views processing, before other tasks..  
Adding output to the view can be accomplished by placing text on $view-&gt;attachment\_before and $view-&gt;attachment\_after.

_**hook\_views\_pre\_view\(&$view, &$display\_id, &$args\)**_

  
**Parameters**

**$view:** The view object which is about to be processed.

**$display\_id:** The machine name of the active display.

**$args:** An array of arguments passed to the view.

**hook\_views\_pre\_build**  
This hook is called right before the build process, but after displays are attached and the display performs its pre\_execute phase.  
We can add output to the view by placing text on $view-&gt;attachment\_before and $view-&gt;attachment\_after.

_**hook\_views\_pre\_build\(&$view\)**_

**Parameters**

**$view:** The view object about to be processed.

**hook\_views\_post\_build**  
This hook is called right after the build process. The query has been fully built now, but it has not yet been run through db\_rewrite\_sql.

Adding output to the view can be accomplished by placing text on $view-&gt;attachment\_before and $view-&gt;attachment\_after.  
 

_**hook\_views\_post\_build\(&$view\)**_

**Parameters**

**$view:** The view object about to be processed.

**hook\_views\_pre\_execute**  
This hook is called right before the execution process. The query has now been fully built, but it has not yet been run through db\_rewrite\_sql.

Adding output to the view can be accomplished by placing text on $view-&gt;attachment\_before and $view-&gt;attachment\_after.

_**hook\_views\_pre\_execute\(&$view\)**_  
      
**Parameters**

**$view:** The view object about to be processed.

**Hook\_views\_post\_execute**  
This hook is called right after the executing process. The query is now executed, but the pre\_render\(\) phase has not yet been executed for handlers.

Adding output to the view can be accomplished by placing text on $view-&gt;attachment\_before and $view-&gt;attachment\_after. Altering the content can be achieved by editing the items of $view-&gt;result.

_**hook\_views\_post\_execute\(&$view\)**_

**Parameters**  
 

**$view:** The view object about to be processed.

**hook\_views\_pre\_render**  
The Drupal views pre-render is called right before the rendering process. The query has been executed, and the pre\_render\(\) phase has already happened for handlers, so all data should be available.

Adding output to the view can be accomplished by placing text on $view-&gt;attachment\_before and $view-&gt;attachment\_after. Altering the content can be achieved by editing the items of $view-&gt;result.

This hook can be utilized by themes.

_**hook\_views\_pre\_render\(&$view\)**_

**Parameters**

**$view:** The view object about to be processed.  
 

**hook\_views\_post\_render**  
Post process any rendered data.

This can be valuable to be able to cache a view and still have some level of dynamic output. In an ideal world, the actual output will include HTML comment based tokens, and then the post process can replace those tokens.

_**hook\_views\_post\_render\(&$view, &$output, &$cache\)**_

**Parameters**

**$view:** The view object about to be processed.

**$output:** A flat string with the rendered output of the view.

**$cache:** The cache settings.

  
All the above phases have a generic flow that ‘view’ follows. Altering a view query to get your choice of data or the output which is not feasible to get it from existing views configuration could be very easy by understanding these phases.
