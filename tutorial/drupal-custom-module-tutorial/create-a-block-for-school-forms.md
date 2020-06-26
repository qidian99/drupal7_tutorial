# Create a block for school register form

## Implement the `block_info` hook

{% code title="schools.module" %}
```php
/**
 * Implements hook_block_info().
 */
function schools_block_info()
{
  $blocks['create'] = array(
    // The name that will appear in the block list.
    'info' => t('Register a school'),
    // Default setting.
    'cache' => DRUPAL_CACHE_PER_ROLE,
    // 'status' => TRUE,
    // 'region' => 'Content',
    // 'visibility' => BLOCK_VISIBILITY_LISTED,
    // 'pages' => 'schools',

    // To change the visibility of the block, use 'visibility' and 'pages'.
    // 'status' => TRUE,
    // 'region' => 'Content',
    // 'visibility' => BLOCK_VISIBILITY_LISTED,
    // 'pages' => 'node/*',

    // another option
    // 'visibility' => BLOCK_VISIBILITY_PHP,
    // 'pages' => 'PHP_CODE',
  );
  $blocks['list'] = array(
    'info' => t('List all schools'),
    'cache' => DRUPAL_CACHE_PER_ROLE,
  );
  return $blocks;
}
```
{% endcode %}

This will show the defined blocks inside `Structure - Blocks` , but it does not define the content to render within the block. To do that, another hook needs to be implemented.

## Implement the `block_view` hook

{% code title="schools.module" %}
```php
function schools_block_view($delta = '')
{

  // This example is adapted from node.module.
  $block = array();
  switch ($delta) {
    case 'create':
      $block['subject'] = t('Register a school');
      $form = drupal_get_form('schools_form', 'block');
      $block['content'] = drupal_render($form);
      break;
    case 'list':
      $block['content'] = t('List of all schools.');
      break;
  }
  return $block;
}
```
{% endcode %}

When we have the form `Register a school`, the delta variable will be `create`, and we telling the function to render the register form as in `schools/create`

## Implement the `info_alter` hook

To fix the position/region of a block \(w.r.t. the current theme layout\), we need to interpolate whenever the block info is saved into database so that the block is immutable and apply only to one specific page \(`schools`\)

{% code title="schools.module" %}
```php
/**
 * Implements hook_block_info_alter().
 */
function schools_block_info_alter(&$blocks, $theme, $code_blocks)
{

  if (isset($blocks['schools']['create'])) {

    // list of regions: https://www.drupal.org/project/drupal/issues/1172560
    $blocks['schools']['create']['status'] = 1;
    $blocks['schools']['create']['region'] = 'sidebar_second';
    $blocks['schools']['create']['weight'] = 0;
    $blocks['schools']['create']['visibility'] = BLOCK_VISIBILITY_LISTED;
    $blocks['schools']['create']['pages'] = 'schools';

  }
}
```
{% endcode %}

## Customize the style of register form

Re-define the register form to be

{% code title="schools.module" %}
```php
function schools_form($form, &$form_state, $type = 'page')
{
  $form['name'] = array(
    '#type' => 'textfield',
    '#title' => 'Name',
    '#required' => TRUE,
    '#attributes' => array('class' => array('create-form__name')),
    '#prefix' => '<div class="create-form__field">',
    '#suffix' => '</div>'
  );

  $form['address'] = array(
    '#type' => 'textfield',
    '#title' => 'Address',
    '#required' => TRUE,
    '#attributes' => array('class' => array('create-form__address')),
    '#prefix' => '<div class="create-form__field">',
    '#suffix' => '</div>'
  );

  $form['zip_code'] = array(
    '#type' => 'textfield',
    '#title' => 'Zip Code',
    '#required' => TRUE,
    '#size' => 5,
    '#maxlength' => 5,
    '#attributes' => array('class' => array('create-form__zip_code')),
    '#prefix' => '<div class="create-form__field">',
    '#suffix' => '</div>'
  );

  $form['submit_button'] = array(
    '#type' => 'submit',
    '#value' => t('Register'),
    '#attributes' => array('class' => array('create-form__submit')),
  );

  // dd($type);
  // _form_set_class($form, array('schools-' . $type));

  return $form;
}
```
{% endcode %}

while leaving the other two functions/hooks unchanged.

Change `school-forms.css` to be

{% code title="school-forms.css" %}
```css
.edit-form__name {
  font-family: Roboto;
  font-style: normal;
  font-weight: bold;
  font-size: 23px;
  line-height: 27px;
  width: calc(90% - 130px);
}

.create-form__name,
.create-form__address,
.create-form__zip_code {
  background-color: #E4E3E3 !important;
}

.create-form__name,
.create-form__address,
.create-form__zip_code,
.edit-form__address,
.edit-form__zip_code {
  background: #EDEDED;
  width: 90%;
  padding: 8px;
  color: #6E6E6E;
  border: 0px !important;
}

.edit-form__field label {
  font-family: Roboto;
  font-style: normal;
  font-weight: bold;
  font-size: 16px !important;
  line-height: 19px;
  margin-bottom: 10px;
}

.edit-form__submit {
  padding: 8px !important;
  width: 100px;
  border-radius: 6px !important;
  background: #C4C4C4 !important;
  border: 0px !important;
  color: #0A8BC2 !important;
  font-weight: bold !important;
  position: absolute;
  right: 80px;
  top: 0px;
}

.create-form__submit {
  height: 36px;
  left: 495px;
  top: 281px;
  background-color: #C4C4C4 !important;
  border-radius: 6px !important;
}

/* .schools-block .create-form__submit:nth-of-type(1) { */

.schools-block .create-form__submit {
  color: black;
  width: 100%;
}

/* For the block title */
#block-schools-create {
  font-weight: bold;
  background-color: #EDEDED;
  padding-right: 50px
}

/* For edit form */
#schools-edit-form {
  position: relative;
}
```
{% endcode %}

## Result

The register form will be rendered in the block that is placed in the secondary sidebar, only in `/schools`

![](../../.gitbook/assets/image%20%2819%29.png)

In the page `/schools/create` The form will look different, since we are passing an extra `type` argument to the form hook and add different classes for styling.

![](../../.gitbook/assets/image%20%2820%29.png)

