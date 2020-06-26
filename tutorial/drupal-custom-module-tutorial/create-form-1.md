# Create form for insertion, update, and deletion

{% embed url="https://www.drupal.org/docs/7/howtos/how-to-make-a-simple-module-with-a-form-and-menu-link" caption="Reference" %}

## Create form for registering schools

### Modify the `schools_menu` hook

Add the following entry to items

{% code title="schools.module:schools\_menu\(\)" %}
```php
$items['schools/create'] = array(
    'title' => 'Register a School',
    'description' => 'Insert a new school in the Schools table',
    'page callback' => 'drupal_get_form', // For a form, use drupal_get_form
    'page arguments' => array('schools_form'), //put the name of the form here
    'access callback' => TRUE,
  );
```
{% endcode %}

### Add three functions for the create form

Note the naming rule is `FORM_NAME`, `FORM_NAME_submit`, and `FORM_NAME_validate`

Within `schools.module`:

{% tabs %}
{% tab title="schools\_form" %}
```php
function schools_form($form, &$form_state)
{


  $form['name'] = array(
    '#type' => 'textfield',
    '#title' => 'Name',
    '#required' => TRUE,
  );

  $form['address'] = array(
    '#type' => 'textfield',
    '#title' => 'Address',
    '#required' => TRUE,
  );

  $form['zip_code'] = array(
    '#type' => 'textfield',
    '#title' => 'Zip Code',
    '#required' => TRUE,
    '#size' => 5,
    '#maxlength' => 5,
  );

  $form['submit_button'] = array(
    '#type' => 'submit',
    '#value' => t('Register'),
  );

  return $form;
}
```
{% endtab %}

{% tab title="schools\_form\_validate" %}
```php
function schools_form_validate($form, &$form_state)
{
  if (!ctype_digit($form_state['values']['zip_code'])) {
    form_set_error('zip_code', t('Please enter a valid zip code.'));
  }
}
```
{% endtab %}

{% tab title="schools\_form\_submit" %}
```php
function schools_form_submit($form, &$form_state)
{
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

  drupal_goto("/schools/" . $sid);
}
```
{% endtab %}
{% endtabs %}

### Result 

Example of `http://drupal-7-72.dd:8083/schools/create`

![](../../.gitbook/assets/image%20%287%29.png)

## Create form for editing school

### Modify the `schools_menu` hook

Add the following entry to items

{% code title="schools.module:schools\_menu\(\)" %}
```php
 $items['schools/%/edit'] = array(
    'title' => 'Edit the information of a school',
    'page callback' => 'drupal_get_form',
    'page arguments' => array('schools_edit_form', 1),
    'access callback' => TRUE,
  );
```
{% endcode %}

### Add three functions for the edit form

Note the naming rule is `FORM_NAME`, `FORM_NAME_submit`, and `FORM_NAME_validate`

Within `schools.module`:

{% tabs %}
{% tab title="schools\_edit\_form" %}
```php
function schools_edit_form($form, &$form_state, $sid)
{
  if (ctype_digit($sid)) {
    $query = db_select('schools', 's')
      ->fields('s')
      ->condition('sid', $sid); // equal by default

    $result = $query->execute();

    if ($result->rowCount() == 1) {
      $school = $result->fetchObject();

      $form['sid'] = array(
        '#type' => 'hidden',
        '#value' => $sid
      );

      $form['name'] = array(
        '#type' => 'textfield',
        '#title' => t('Name'),
        '#default_value' => $school->name,
        '#required' => TRUE,
      );

      $form['address'] = array(
        '#type' => 'textfield',
        '#title' => t('Address'),
        '#default_value' => $school->address,
        '#required' => TRUE,
      );

      $form['zip_code'] = array(
        '#type' => 'textfield',
        '#title' => t('Zip Code'),
        '#default_value' => $school->zip_code,
        '#required' => TRUE,
        '#size' => 5,
        '#maxlength' => 5,
      );

      $form['submit'] = array(
        '#type' => 'submit',
        '#value' => t('Update school information'),

      );
      return $form;
    } else {
      return 'School does not exist';
    }
  }
}
```
{% endtab %}

{% tab title="schools\_form\_validate" %}
```php
function schools_edit_form_validate($form, &$form_state)
{
  schools_form_validate($form, $form_state);
}
```
{% endtab %}

{% tab title="schools\_form\_submit" %}
```php
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
```
{% endtab %}
{% endtabs %}

### Result

Example of `http://drupal-7-72.dd:8083/schools/21/edit`

![](../../.gitbook/assets/image%20%289%29.png)

## Create form for deleting school

### Modify the `schools_menu` hook

Add the following entry to items

{% code title="schools.module:schools\_menu\(\)" %}
```php
$items['schools/%/delete'] = array(
    'title' => 'Delete school',
    'page callback' => 'drupal_get_form',
    'page arguments' => array('school_delete_form', 1),
    'access arguments' => array('delete schools'),
    'access callback' => TRUE,
  );
```
{% endcode %}

### Add two functions for the delete form

Note the naming rule is `FORM_NAME`, `FORM_NAME_submit`, and `FORM_NAME_validate`

Within `schools.module`:

{% tabs %}
{% tab title="school\_delete\_form" %}
```php
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
```
{% endtab %}

{% tab title="school\_delete\_form\_submit" %}
```php
function school_delete_form_submit($form, &$form_state)
{
  delete_school($form['#sid']);
}
```
{% endtab %}
{% endtabs %}

### Result

Example of `http://drupal-7-72.dd:8083/schools/21/delete`

![](../../.gitbook/assets/image%20%2810%29.png)

