# Code Summary

## Custom module

`DRUPAL_ROOT/sites/all/modules/custom/schools`

{% tabs %}
{% tab title="schools.info" %}
```text
name = Schools
description = "Provides CRUD operations for school data"
core = 7.x
; If your module comes with other modules or is meant to be used exclusively with other modules, enter the name of the package here. If left blank, the module will be listed as 'Other'. In general, this property should only be used by large multi-module packages, or by modules meant to extend these packages
; package = Views

; dependencies[] = modal_forms (>1.2+25-dev)

; Drupal supports a dynamic-loading code registry. To support it, all modules must declare any code files containing class or interface declarations in the .info file, like so
; When a module is enabled, Drupal will rescan all declared files and index all the classes and interfaces that it finds. Classes will be loaded automatically by PHP when they are first accessed.
; files[] = tests/example.test

; Drupal 7 allows you to add CSS files in the module's .info file if it should be added on every page, just like theme .info files do. Here is an example from the node module's .info file:
; stylesheets[all][] = node.css
stylesheets[all][] = school.css
stylesheets[all][] = school-forms.css

; ; Add a style sheet for all media
; stylesheets[all][] = theStyle.css

; ; Add a style sheet for screen and projection media
; stylesheets[screen, projection][] = theScreenProjectionStyle.css

; ; Add a style sheet for print media
; stylesheets[print][] = thePrintStyle.css

; ; Add a style sheet with media query
; stylesheets[screen and (max-width: 600px)][] = theStyle600.css

; As of version 7.x, the path of the module's (main) configuration page. If a module is enabled, a "Configure" and "Permissions" link appear. This will be the path of the "Configure" link for this particular module on the modules overview page.
configure = admin/config/content/school

```
{% endtab %}

{% tab title="schools.install" %}
```php
<?php

function schools_schema()
{
  $schema['schools'] = array(
    'description' => 'The schools table',
    'fields' => array(
      'sid' => array(
        'description' => 'The primary identifier for a school.',
        'type' => 'serial',
        'unsigned' => TRUE,
        'not null' => TRUE),
      'name' => array(
        'description' => 'The name of the school.',
        'type' => 'varchar',
        'length' => 255,
        'not null' => TRUE,
        'default' => ''
      ),
      'address' => array(
        'description' => 'The address of the school',
        'type' => 'varchar',
        'length' => 255,
        'not null' => TRUE,
        'default' => ''
      ),
      'zip_code' => array(
        'description' => 'The zip code of the school.',
        'type' => 'varchar',
        'length' => 32,
        'not null' => TRUE,
        'default' => '00000'
      ),
    ),
    'indexes' => array(
      'school_names'        => array('name'),
      'school_ids'        => array('sid'),
    ),
    'unique keys' => array(
      'name_sid' => array('name', 'sid'),
      'sid'     => array('sid')
    ),
    'primary key' => array('sid'),
  );
  return $schema;
}

```
{% endtab %}

{% tab title="schools.module" %}
```php
<?php

require_once("schools.theme.inc"); // at the top of schools.module
require_once('schools.modal.inc');

// ---------------- hooks -------------------

// To make a path, you need to create a Drupal hook_menu function. ‘Hook’ indicates the name of the module, so in our case the function’s name will be books_menu()
/**
 * implement hook_menu()
 * create menu item
 * schools_menu function will create a menu item which can be access with localhost/path/to/schools
 */
function schools_menu()
{
  $items = array();
  $items['schools'] = array(
    'title'             =>  'Schools',  // page title
    'description'       =>  'Schools Information',  // description show when mouse hover on link
    'page callback'     =>  'schools_list',  // callback function which is invoked when menu item is called.
    'access callback'   =>  TRUE,  // any user can access this page
  );

  $items['schools/%'] = array(
    // 'title'             =>  'School',
    'description'       =>  'School Information',
    'page callback' => 'schools_view_item_page',
    'access callback'   =>  TRUE,
    'page arguments' => array(
      1,
    ),
  );

  $items['schools/create'] = array(
    'title' => 'Register a School',
    'description' => 'Insert a new school in the Schools table',
    'page callback' => 'drupal_get_form', // For a form, use drupal_get_form
    'page arguments' => array('schools_form'), //put the name of the form here
    'access callback' => TRUE,
  );
  $items['schools/%/edit'] = array(
    // 'title' => 'Edit the information of a school',
    'page callback' => 'schools_edit_item_page',
    'page arguments' => array(
      1
    ),
    // 'page arguments' => array('schools_edit_form', 1),
    'access callback' => TRUE,
  );

  $items['schools/%/delete'] = array(
    'title' => 'Delete school',
    'page callback' => 'drupal_get_form',
    'page arguments' => array('school_delete_form', 1),
    'access arguments' => array('delete schools'),
    'access callback' => TRUE,
    // 'type' => MENU_LOCAL_TASK,
  );


  $items['test'] = array(
    'page callback' => 'mymodule_page',
    'access callback' => TRUE,
    'type' => MENU_CALLBACK,
  );

  $items['schools/forms/%ctools_js'] = array(
    'page callback' => 'mymodule_callback',
    'page arguments' => array(1),
    'access callback' => TRUE,
    'type' => MENU_CALLBACK,
  );

  return $items;
}

/**
 * Implements hook_admin_paths_alter().
 */
function schools_admin_paths_alter(&$paths)
{
  // $paths['schools/create'] = TRUE;
}


/**
 * Implement the hook_preprocess_get_school:
 */
function schools_preprocess_get_school(&$variables)
{
  $variables['delete_cb'] = 'delete_cb';
}


/*
https://www.drupal.org/forum/support/post-installation/2010-05-12/how-can-i-enable-a-block-programmatically
An issue with hook_block_info_alter() is that it prevents future changes, as the hook will fire every time blocks or block configuration is saved. So in your example above, if you changed the region of the block in the UI, it would jump back to the Header region.
BartK's solution function allows you to enable blocks and place them on install of an install profile or a module without prohibiting future configuration changes.
*/

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



// ---------------------- functions ---------------------------


function delete_school($sid)
{

  db_delete('schools')
    ->condition('sid', $sid)
    ->execute();

  drupal_goto("/schools");
}


function schools_list()
{
  // select all rows from books table
  $query = db_select('schools', 's')->fields('s');
  // execute above query to get the results from database table.
  $result = $query->execute();
  //send data to custom theme template
  //theme schools_list created under sites\all\themes\bartik\templates\schools\schools-list.tpl.php
  $output = theme('schools_list', array('data' => $result));
  return $output;
}

function schools_view_item_page($sid)
{
  // echo is_int($sid) ? 'true' : 'false';
  // false -- That's weird, actually I'm passing 18 as argument
  // echo ctype_digit($sid) ? 'true' : 'false';
  // true -- this works
  if (ctype_digit($sid)) {
    $query = db_select('schools', 's')
      ->fields('s')
      ->condition('sid', $sid); // equal by default

    $result = $query->execute();

    // echo $result->rowCount();
    // 1
    if ($result->rowCount() == 1) {
      $obj = $result->fetchObject();
      $output = theme('get_school', array('school' => $obj));
      return $output;
    }
    return 'school does not exist';
  }
  return 'invalid school id';
}


function schools_edit_item_page($sid)
{
  $edit_form = drupal_get_form('schools_edit_form', $sid);
  $output = drupal_render($edit_form);
  $output = theme('edit_school', array('form' => $output));
  return $output;
}

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

function schools_form_validate($form, &$form_state)
{
  if (!ctype_digit($form_state['values']['zip_code'])) {
    form_set_error('zip_code', t('Please enter a valid zip code.'));
  }
}

function schools_form_submit($form, &$form_state)
{
  // TODO: need to set debugging/logger to make sure this is working
  // For now, test the redirect to see if it works
  // drupal_goto('/');

  // Dump to /tmp/drupal_debug.txt
  // Array
  // (
  //     [name] => Dian Qi
  //     [address] => 3535 Lebon Dr
  //     [zip_code] => 92122
  //     [submit_button] => Register
  //     [form_build_id] => form-GSQ2zir1jQr8YLSAKpoQ-FrkHuZsropSuigYhV6ga6Q
  //     [form_token] => Xr3lJ2Czm3dy7KJDZJcVQNst9cWCx6qbZZkCk6WIlu0
  //     [form_id] => schools_form
  //     [op] => Register
  // )
  // dd($form_state['values']);

  // create the school record and redirect to the school page
  $name = $form_state['values']['name'];
  $address = $form_state['values']['address'];
  $zip_code = $form_state['values']['zip_code'];

  $sid = db_insert('schools')
    ->fields(array(
      'name' => $name,
      'address' => $address,
      'zip_code' => $zip_code,
    ))
    ->execute();

  // make sure to be the last inserted id
  // dd($sid);

  drupal_goto("/schools/" . $sid);
}


function schools_edit_form($form, &$form_state, $sid)
{
  // Save the node to the form state for use in the submit function
  if (ctype_digit($sid)) {
    $query = db_select('schools', 's')
      ->fields('s')
      ->condition('sid', $sid); // equal by default

    $result = $query->execute();

    // echo $result->rowCount();
    // 1
    if ($result->rowCount() == 1) {
      $school = $result->fetchObject();

      $form['sid'] = array(
        '#type' => 'hidden',
        '#value' => $sid
      );

      $form['name'] = array(
        '#type' => 'textfield',
        '#default_value' => $school->name,
        '#required' => TRUE,
        '#attributes' => array('class' => array('edit-form__name')),
      );

      $form['address'] = array(
        '#type' => 'textfield',
        '#title' => t('Address'),
        '#default_value' => $school->address,
        '#required' => TRUE,
        '#attributes' => array('class' => array('edit-form__address')),
        '#prefix' => '<div class="edit-form__field">',
        '#suffix' => '</div>'
      );

      $form['zip_code'] = array(
        '#type' => 'textfield',
        '#title' => t('Zip Code'),
        '#default_value' => $school->zip_code,
        '#required' => TRUE,
        '#size' => 5,
        '#maxlength' => 5,
        '#attributes' => array('class' => array('edit-form__zip_code')),
        '#prefix' => '<div class="edit-form__field">',
        '#suffix' => '</div>'
      );

      $form['submit'] = array(
        '#type' => 'submit',
        '#value' => t('Done'),
        '#attributes' => array('class' => array('edit-form__submit')),

      );
      return $form;
    } else {
      return 'School does not exist';
    }
  }
}

function schools_edit_form_validate($form, &$form_state)
{
  schools_form_validate($form, $form_state);
}

function schools_edit_form_submit($form, &$form_state)
{

  $sid = $form_state['values']['sid'];
  $name = $form_state['values']['name'];
  $address = $form_state['values']['address'];
  $zip_code = $form_state['values']['zip_code'];

  db_update('schools')
    ->fields(array(
      'name' => $name,
      'address' => $address,
      'zip_code' => $zip_code,
    ))
    ->condition('sid', $sid)
    ->execute();

  // make sure to be the last inserted id
  // dd($sid);

  drupal_goto("/schools/" . $sid);
}


function school_delete_form($form, &$form_state, $sid)
{
  $form['#sid'] = $sid;
  // Note confirm_form() can be used here, but I prefer to use my own for styling purposes
  $form['header'] = array(
    '#markup' => t('Are you sure you wish to delete the school with id <em>@value</em>?', array('@value' => $sid)),
    '#prefix' => '<h2>',
    '#suffix' => '</h2>',
  );
  $form['warning'] = array(
    '#markup' => t('Warning, this action cannot be undone'),
    '#prefix' => '<p>',
    '#suffix' => '</p>',
  );
  $form['delete_button'] = array(
    '#type' => 'submit',
    '#value' => t('Delete item'),
  );
  return $form;
}

function school_delete_form_submit($form, &$form_state)
{
  delete_school($form['#sid']);
}

```
{% endtab %}

{% tab title="schools.modal.inc" %}
```php
<?php

/**
 * Helper function to make a link.
 */
function _mymodule_make_link($link_text = '')
{
  // Set a default value if no text in supplied.
  if (empty($link_text)) {
    $link_text = 'Magical Modal';
  }

  return '<div id="magical-modal-link">' . l($link_text, 'schools/forms/nojs', array('attributes' => array('class' => 'ctools-use-modal'))) . '</div>';
}

/**
 * Drupal form to be put in a modal.
 */
function mymodule_form($form, $form_state)
{
  $form = array();

  $form['new_link_text'] = array(
    '#type' => 'textfield',
    '#title' => t('Link text'),
  );

  $form['submit'] = array(
    '#type' => 'submit',
    '#value' => t('Submit'),
  );

  return $form;
}

/**
 * An example page.
 */
function mymodule_page()
{
  // Load the modal library and add the modal javascript.
  ctools_include('modal');
  ctools_modal_add_js();
  return _mymodule_make_link('Magical modal');
}

/**
 * Ajax menu callback.
 */
function mymodule_callback($ajax)
{
  if ($ajax) {
    ctools_include('ajax');
    ctools_include('modal');

    $form_state = array(
      'ajax' => TRUE,
      'title' => t('MyModule Modal Form'),
    );

    // Use ctools to generate ajax instructions for the browser to create
    // a form in a modal popup.
    $output = ctools_modal_form_wrapper('mymodule_form', $form_state);

    // If the form has been submitted, there may be additional instructions
    // such as dismissing the modal popup.
    if (!empty($form_state['ajax_commands'])) {
      $output = $form_state['ajax_commands'];
    }

    // Return the ajax instructions to the browser via ajax_render().
    print ajax_render($output);
    drupal_exit();
  } else {
    return drupal_get_form('mymodule_form');
  }
}

/**
 * Drupal form submit handler.
 */
function mymodule_form_submit(&$form, &$form_state)
{
  // Generate the new link using the submitted text value.
  $link = _mymodule_make_link($form_state['values']['new_link_text']);

  // Tell the browser to close the modal.
  $form_state['ajax_commands'][] = ctools_modal_command_dismiss();

  // Tell the browser to replace the old link with the new one.
  $form_state['ajax_commands'][] = ajax_command_replace('#magical-modal-link', $link);
}

```
{% endtab %}

{% tab title="schools.theme.inc" %}
```php
<?php
/*
 * hook_menu to load tpl files from theme folder
 * i.e sites/all/themes/custom/{current_theme_name}/templates/books
 * current_theme_name = fiction 
 */
function schools_theme()
{
  // themes/bartik
  $path_to_theme = drupal_get_path('theme', variable_get('theme_default', 'schools'));
  $themes = array();
  $themes['schools_list'] = array(
    'template' => 'schools-list',
    'path' => $path_to_theme . '/templates/schools',
  );
  $themes['get_school'] = array(
    'template' => 'get-school',
    'path' => $path_to_theme . '/templates/schools',
  );
  $themes['edit_school'] = array(
    'template' => 'edit-school',
    'path' => $path_to_theme . '/templates/schools',
  );
  return $themes;
}
```
{% endtab %}

{% tab title="school-forms.css" %}
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
{% endtab %}

{% tab title="schools.css" %}
```

```
{% endtab %}
{% endtabs %}

## Theme & Template

`DRUPAL_ROOT/themes/bartik/templates/schools/`

{% tabs %}
{% tab title="school-list.tpl.php" %}
```php
<?php

drupal_add_js(drupal_get_path('module', 'schools') . '/school-list.js');

echo "<div class='schools-list'>";
if ($data->rowCount() > 0) {
  foreach ($data as $v) {
    echo "<div class='school' onclick=" . "'window.location.href = \"/schools/" . $v->sid . "\"'"  . ">";
    echo "<div class='school__name'>" . $v->name . "</div>";
    echo "<div class='school__addr_label'>Address</div>";
    echo "<div class='school__address'>" . $v->address . "</div>";
    echo "<div class='school__button_container'>
        <button class='school__edit_button' onclick='window.location.href=\"" . "/schools/" . $v->sid . "/edit\";event.cancelBubble=true;'>Edit</button>";
    echo "<button class='school__delete_button' onclick='window.location.href=\"" . "/schools/" . $v->sid . "/delete\";event.cancelBubble=true;'>Delete</button></div>";
    echo "</div>";
  }
} else {
  echo "No records found";
}

echo '</div>';

```
{% endtab %}

{% tab title="get-school.tpl.php" %}
```php
<div class="school-name"><?php echo $school->name ?></div>

<div class="school-field">
  <div class="school-field__label">School ID</div>
  <div class="school-field__value"><?php echo $school->sid ?></div>
</div>
<div class="school-field">
  <div class="school-field__label">School Address</div>
  <div class="school-field__value"><?php echo $school->address ?></div>
</div>
<div class="school-field">
  <div class="school-field__label">Zip Code</div>
  <div class="school-field__value"><?php echo $school->zip_code ?></div>
</div>

<div class="buttons">
  <button class="edit-button" onclick="window.location.href='/schools/<?php echo $school->sid ?>/edit'">Edit</button>
  <button class="delete-button" onclick="window.location.href='/schools/<?php echo $school->sid ?>/delete'">Delete</button>
</div>
<?php

```
{% endtab %}

{% tab title="edit-school.tpl.php" %}
```php
<?php
echo $form;
```
{% endtab %}
{% endtabs %}



