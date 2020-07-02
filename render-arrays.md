---
description: Mostly dealing with "Render Arrays"
---

# UI Implementation

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

## Turn "Off" caching

{% embed url="https://drupal.stackexchange.com/questions/28340/how-to-completely-turn-off-caching" %}

## Container

{% embed url="https://drupal.stackexchange.com/questions/16831/how-do-i-wrap-two-render-array-elements-in-a-div" %}

{% embed url="https://medium.com/@robleto/how-to-set-internal-border-lines-on-a-css-grid-layout-f2f1eeaafb61" %}

## css dynamic height with maximum number of columns

### animation

{% embed url="https://developer.mozilla.org/en-US/docs/Web/CSS/CSS\_Columns/Using\_multi-column\_layouts" %}

```javascript
const percentage = $(circle).attr('data-percentage');
const radius = circle.r.baseVal.value;
const circumference = radius * 2 * Math.PI;

function setProgress(percent) {
  const offset = circumference - percent / 100 * circumference;
  circle.style.strokeDashoffset = offset;
}

setProgress(percentage);
```

## Template proprocessing

### linear gradient to stroke

{% embed url="https://www.drupal.org/docs/7/theming/overriding-themable-output/setting-up-variables-for-use-in-a-template-preprocess-and" %}

{% embed url="https://vanseodesign.com/web-design/svg-linear-gradients/" %}

## Build the CSS 

## HTML related

{% embed url="https://css-tricks.com/building-progress-ring-quickly/" %}

### span vs. div

{% embed url="https://api.drupal.org/api/drupal/modules%21block%21block.api.php/function/hook\_block\_view/7.x" %}

> The difference between [`span`](https://htmldog.com/references/html/tags/span/) and [`div`](https://htmldog.com/references/html/tags/div/) is that a [`span`](https://htmldog.com/references/html/tags/span/) element is **in-line** and usually used for a small chunk of HTML inside a line \(such as inside a paragraph\) whereas a [`div`](https://htmldog.com/references/html/tags/div/) \(division\) element is **block-line** \(which is basically equivalent to having a line-break before and after it\) and used to group larger chunks of code.

## Manage JS



{% embed url="https://www.drupal.org/docs/7/api/javascript-api/managing-javascript-in-drupal-7" %}

## chart

{% embed url="http://www.coding-dude.com/wp/html5/bar-chart-html/" %}

## SVG

### Build the circle percentage

[https://css-tricks.com/building-progress-ring-quickly/](https://css-tricks.com/building-progress-ring-quickly/)



### Change svg background color

{% embed url="https://stackoverflow.com/questions/22252472/how-to-change-the-color-of-an-svg-element\#:~:text=You%20can\'t%20change%20the,or%20using%20inline." %}





