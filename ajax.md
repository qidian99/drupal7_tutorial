# Ajax

## Ajax callback

{% embed url="https://www.drupal.org/docs/7/api/javascript-api/simple-drupal-ajax-load-with-jquery-and-delivery-callback" %}

> The real trick here is to get only the HTML you need instead of rendering the header, footer, and every other element that comes with a full page load. This is where the 'delivery callback' setting in [hook\_menu](https://api.drupal.org/api/drupal/modules!system!system.api.php/function/hook_menu/7) comes into play. The 'delivery callback' setting defaults to [drupal\_deliver\_html\_page\(\)](https://api.drupal.org/api/drupal/includes!common.inc/function/drupal_deliver_html_page/7) which returns a fully rendered HTML page. We need to define our own delivery callback function returning just the HTML we want to render via AJAX on the client side.



{% embed url="https://www.drupal.org/docs/7/api/javascript-api/ajax-forms-in-drupal-7" %}

## Onclick conflict

{% embed url="http://www.maged.me/blog/drupal-7-execute-javascript-code-after-ajax-call" %}





## Add images within link

{% embed url="https://api.drupal.org/api/examples/ajax\_example%21ajax\_example\_misc.inc/function/ajax\_example\_render\_link/7.x-1.x" %}

```php
'#markup' => l(t('Click here'), 'dev/dc4/ajax/admins/nojs', array(
  'attributes' => array(
    'class' => array(
      'use-ajax',
    ),
  ),
))
```

{% code title="common.inc" %}
```php
function l($text, $path, array $options = array()) {
  global $language_url;
  static $use_theme = NULL;

  // Merge in defaults.
  $options += array(
    'attributes' => array(),
    'html' => FALSE,
  );

  // Append active class.
  if (($path == $_GET['q'] || ($path == '<front>' && drupal_is_front_page())) &&
      (empty($options['language']) || $options['language']->language == $language_url->language)) {
    $options['attributes']['class'][] = 'active';
  }

  // Remove all HTML and PHP tags from a tooltip. For best performance, we act only
  // if a quick strpos() pre-check gave a suspicion (because strip_tags() is expensive).
  if (isset($options['attributes']['title']) && strpos($options['attributes']['title'], '<') !== FALSE) {
    $options['attributes']['title'] = strip_tags($options['attributes']['title']);
  }

  // Determine if rendering of the link is to be done with a theme function
  // or the inline default. Inline is faster, but if the theme system has been
  // loaded and a module or theme implements a preprocess or process function
  // or overrides the theme_link() function, then invoke theme(). Preliminary
  // benchmarks indicate that invoking theme() can slow down the l() function
  // by 20% or more, and that some of the link-heavy Drupal pages spend more
  // than 10% of the total page request time in the l() function.
  if (!isset($use_theme) && function_exists('theme')) {
    // Allow edge cases to prevent theme initialization and force inline link
    // rendering.
    if (variable_get('theme_link', TRUE)) {
      drupal_theme_initialize();
      $registry = theme_get_registry(FALSE);
      // We don't want to duplicate functionality that's in theme(), so any
      // hint of a module or theme doing anything at all special with the 'link'
      // theme hook should simply result in theme() being called. This includes
      // the overriding of theme_link() with an alternate function or template,
      // the presence of preprocess or process functions, or the presence of
      // include files.
      $use_theme = !isset($registry['link']['function']) || ($registry['link']['function'] != 'theme_link');
      $use_theme = $use_theme || !empty($registry['link']['preprocess functions']) || !empty($registry['link']['process functions']) || !empty($registry['link']['includes']);
    }
    else {
      $use_theme = FALSE;
    }
  }
  if ($use_theme) {
    return theme('link', array('text' => $text, 'path' => $path, 'options' => $options));
  }
  // The result of url() is a plain-text URL. Because we are using it here
  // in an HTML argument context, we need to encode it properly.
  return '<a href="' . check_plain(url($path, $options)) . '"' . drupal_attributes($options['attributes']) . '>' . ($options['html'] ? $text : check_plain($text)) . '</a>';
}
```
{% endcode %}

* html is boolean, if true then we don't check\_plain the text

Or use these:

```php
$image = theme('image', array('path' => 'images/link1img.png'));

$link = array(
  '#type'    => 'link',
  '#title'   => $image,
  '#href'    => 'http://www.link1.example',
  '#options' => array('html' => TRUE, 'title' => 'link1'),
  '#suffix'  => '<br />',
);
```

{% embed url="https://www.drupal.org/forum/support/module-development-and-code-questions/2013-09-04/ajax-form-submission" %}



## Attach JS to page

### For Drupal 7

```php
$element['#attached']['js'][] = array(
  'data' => array('myModule' => array('basePath' => base_path())), 
  'type' => 'setting',
);
```

This variable would then be referenced from JS side like:

```javascript
Drupal.settings.myModule.basePath;
```

\[1\]: [https://www.drupal.org/node/172169](https://www.drupal.org/node/172169)

Or

```php
drupal_add_js(array('isd_dc4' => array('menus' => ISD_DC4_DEFAULT_MENU)), array('type' => 'setting')),
```

### For Drupal 8

`drupal_add_js()` was removed \(it was deprecated in Drupal 7 already\) =&gt; [see this for further information](https://www.drupal.org/node/2169605).

The way to send PHP information to Javascript is perfectly described \[by @4k4's answer\]\[2\] to a similar question.

```text
return [
  '#theme' => 'item_list',
  '#list_type' => 'ul',
  '#items' => $my_items,
  '#attributes' => ['class' => 'some_class'],
  '#attached' => [
    'library' => ['my_module/my_library'],
    'drupalSettings' => [
      'my_library' => [
        'some_variable1' => $value,        // <== Variables passed
        'another_variable' => $take_this,  // <== 
      ],
    ],
  ],
];
```

In JavaScript, they can be used as follows:

```text
(function ($, Drupal, drupalSettings) {
  Drupal.behaviors.my_library = {
    attach: function (context, settings) {

      alert(drupalSettings.my_library.some_variable); //alerts the value of PHP's $value

    }
  };
})(jQuery, Drupal, drupalSettings);
```

\[2\]: [https://drupal.stackexchange.com/a/211737/74748](https://drupal.stackexchange.com/a/211737/74748)

{% embed url="https://drupal.stackexchange.com/questions/193202/how-do-i-pass-variables-to-javascript" %}



## AJAX on the fly

{% embed url="https://www.drupal.org/docs/7/api/javascript-api/creating-custom-drupalajax-object-on-the-fly-and-attach-it-to-any-dom" %}



```javascript
function ($) {
    'use strict';
    Drupal.behaviors.ajaxConfirmLink = {
      attach: function (context, settings) {
        $('.isd-dc4-menus__atag', context).once('isd-dc4-menus__atag').on('click', function (event) {
          var $this = $(this);
          // Allow to provide confirmation message in
          // data-use-ajax-confirm-message element attribute.

          const index = $('.isd-dc4-menus__atag').index($this);
          console.log(index);

          const id = 'isd-dc4-menu-' + index;

          if (!Drupal.ajax[id]) {
            Drupal.ajax[id] = new Drupal.ajax(id, this, {
              // 'nojs' to 'ajax' replacement in path performed by Drupal.ajax().
              url: $this.attr('data-href'),
              event: 'load_subpage',
              progress: false,
              effect: 'fade',
            });
          }

          $this.trigger('load_subpage');
        });
      }
    };
  }(jQuery)
```



