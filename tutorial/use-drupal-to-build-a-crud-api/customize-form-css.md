# Customize form CSS

## Change the menu hook

{% code title="schools.modules:schools\_menu" %}
```php
  $items['schools/%/edit'] = array
    'page callback' => 'schools_edit_item_page',
    'page arguments' => array(
      1
    ),
    'access callback' => TRUE,
  );
```
{% endcode %}

## Add the page callback

{% code title="schools.modules" %}
```php
function schools_edit_item_page($sid)
{
  $edit_form = drupal_get_form('schools_edit_form', $sid);
  $output = drupal_render($edit_form);
  $output = theme('edit_school', array('form' => $output));
  return $output;
}
```
{% endcode %}

## Add the theme

{% code title="schools.theme.inc:schools\_theme" %}
```php
  $themes['edit_school'] = array(
    'template' => 'edit-school',
    'path' => $path_to_theme . '/templates/schools',
  );
```
{% endcode %}

## Add the template for edit form

We can add more elements. Right now it suffices to just echo the form.

```php
<?php
echo $form;
```

## Add the CSS for forms

{% code title="schools.info" %}
```php
stylesheets[all][] = school-forms.css
```
{% endcode %}

{% code title="school-forms.css" %}
```css
.edit-form__name {
  font-family: Roboto;
  font-style: normal;
  font-weight: bold;
  font-size: 23px;
  line-height: 27px;
  width: 300px;
}

.edit-form__address,
.edit-form__zip_code {
  background: #EDEDED;
  width: 300px;
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
  left: 50vw;
  top: 22px;
}

```
{% endcode %}

## Result

Example from `http://drupal-7-72.dd:8083/schools/22/edit`

![](../../.gitbook/assets/image%20%283%29.png)



