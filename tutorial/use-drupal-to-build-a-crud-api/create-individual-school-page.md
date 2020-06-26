# Create individual school page

## Modify the `schools.module`

### Modify the `schools_menu` hook

Add the following entry to items

{% code title="schools.module:schools\_menu\(\)" %}
```php
$items['schools/%'] = array(
    'description'       =>  'School Information',
    'page callback' => 'schools_view_item_page',
    'access callback'   =>  TRUE,
    'page arguments' => array(
      1,
    ),
  );
```
{% endcode %}

### Add new function for the page callback

{% code title="schools.module" %}
```php
function schools_view_item_page($sid)
{
  if (ctype_digit($sid)) {
    $query = db_select('schools', 's')
      ->fields('s')
      ->condition('sid', $sid); // equal by default

    $result = $query->execute();

    if ($result->rowCount() == 1) {
      $obj = $result->fetchObject();
      $output = theme('get_school', array('school' => $obj));
      return $output;
    }
    return 'school does not exist';
  }
  return 'invalid school id';
}

```
{% endcode %}

## Create the template file

`DRUPAL_ROOT/themes/YOUR_THEME/templates/schools/get-school.tpl.php`

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

// dpm($delete_cb);

```

## Add CSS to the .info file

{% code title="schools.info" %}
```text
stylesheets[all][] = school.css
```
{% endcode %}

{% code title="schools.css" %}
```css
.school-field {
  background-color: white;
  padding: 10px;
  margin-bottom: 5px;
}

.school-name {
  font-family: Roboto;
  font-style: normal;
  font-weight: bold;
  font-size: 23px;
  line-height: 27px;
}

.school-field__label {
  font-family: Roboto;
  font-style: normal;
  font-weight: bold;
  font-size: 16px;
}

.school-field__value {
  background: #EDEDED;
  width: 300px;
  padding: 8px;
  color: #8E8E8E;
}

.edit-button {
  padding: 8px;
  width: 100px;
  border-radius: 6px;
  background: #C4C4C4;
  border: 0px;
  color: #0A8BC2;
  font-weight: bold;
}

.delete-button {
  padding: 8px;
  width: 100px;
  border-radius: 6px;
  background: #FF4646;
  border: 0px;
  color: white;
  font-weight: bold;
}

.buttons {
  position: absolute;
  left: 50vw;
  top: 16px;
  display: flex;
  width: 220px;
  justify-content: space-between;
}

```
{% endcode %}

## Result

Example of `http://drupal-7-72.dd:8083/schools/21`

![](../../.gitbook/assets/image%20%281%29.png)



Note that the links for the buttons will not work at this time. They will be functional after creating the form for insertion, update, and deletion.

