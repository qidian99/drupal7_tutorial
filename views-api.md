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

