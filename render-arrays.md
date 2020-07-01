# Render Arrays

{% embed url="https://www.drupal.org/docs/7/api/render-arrays/render-arrays-overview" %}

```php
$output = array(
    'first_para' => array(
      '#type' => 'markup',
      '#markup' => '<p>A paragraph about some stuff…</p>',
    ),
    'second_para' => array(
      '#items' => array('first item', 'second item', 'third item'),
      '#theme' => 'item_list',
    ),
  );
```

```php
$demos = array(
  t('Super simple #markup')  => array(
    '#markup' => t('Some basic text in a #markup (shows basic markup and how it is rendered)'),
  ),

  'prefix_suffix' => array(
    '#markup' => t('This one adds a prefix and suffix, which put a div around the item'),
    '#prefix' => '(prefix)',
    '#suffix' => '(suffix)',
  ),

  'theme for an element' => array(
    'child' => array(
      t('This is some text that should be put together'),
      t('This is some more text that we need'),
    ),
    '#separator' => ' | ',  // Made up for this theme function.
    '#theme' => 'render_example_aggregate',
  ),
);
```

## How to render a block

1. Get the block's module and delta from database
2. Write the following code

```php
$block_object = block_load('block', '2');
$block = _block_get_renderable_array(_block_render_blocks(array($block_object)));
$page = array(
    'content' => [
      'block' => $block,
      'description' => [
        array(
          '#markup' => '<h1>test html</h1>',
          '#attributes' => array(
            'class' => array('my-class'),
          ),
        )
      ]
    ]
  );
```

## How to define page in render array

need page theme function/template right now don't do it

```text

```

## How to add css to blocks

{% embed url="https://www.drupal.org/forum/support/theme-development/2012-09-30/solved-drupal-7-add-cssstylesheet-to-blocks-within" %}

{% embed url="https://www.drupal.org/docs/7/theming/working-with-css/adding-css-to-form-or-page-with-attachments" %}

`#attached` tag:

> Changing the code to be cache-friendly is as simple as removing the call to drupal\_add\_css\(\) and adding the \#attached property with the resource included in the css property of the array you set as its value.

