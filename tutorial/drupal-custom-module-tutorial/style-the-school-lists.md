# Style the school lists

## Modify the template file

{% code title="schools-list.tpl.php" %}
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
{% endcode %}

The Javascript should be put in the same directory as the custom module. It's of no use at this point.

{% code title="school-list.js" %}
```php
// If you need any Javascript functions
```
{% endcode %}

## Modify the CSS file

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

.schools-list {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 32px;
}

.school {
  background: #EDEDED;
  border-radius: 6px;
  padding: 16px 16px;
  position: relative;
}

.school:hover {
  transition: all 0.6s ease-in-out;
	-moz-box-shadow: 0 0 15px rgba(0, 0, 0, .3);
	-webkit-box-shadow: 0 0 15px rgba(0, 0, 0, .3);
	box-shadow: 0 0 15px rgba(0, 0, 0, .3);
	transform: scale(1.03);
}

.school .school__name {
  font-family: Roboto;
  font-style: normal;
  font-weight: bold;
  font-size: 16px;
  color: #000000;
  margin-bottom: 8px;
  text-transform: uppercase;
}

.school .school__addr_label {
  font-family: Roboto;
  font-style: normal;
  font-weight: bold;
  font-size: 14px;

  color: #5E2B2B;
}


.school .school__address {
  font-family: Roboto;
  font-style: normal;
  font-weight: normal;
  font-size: 12px;
  line-height: 14px;
  color: #8E8E8E;
  overflow: hidden;
  text-overflow: ellipsis;
  /* max-height: 28px; */
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  /* width: 50px; */
  width: 180px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  /* padding: 20px; */
  /* font-size: 1.3rem; */
  margin: 0;
  /* background: white; */
  /* resize: horizontal; */
}

.school .school__button_container {
  position: absolute;
  right: 16px;
  bottom: 16px;
}

.school .school__delete_button {
  color: white;
  background: #FF4646;
  border-radius: 5px;
  border: 0px;
  padding-top: 4px;
  padding-bottom: 4px;
  font-weight: bold;
}

.school .school__edit_button {
  margin-right: 8px;
  color: #0A8BC2;
  background: #C4C4C4;
  border-radius: 5px;
  border: 0px;
  padding-top: 4px;
  padding-bottom: 4px;
  font-weight: bold;
}
```
{% endcode %}

## Result

![](../../.gitbook/assets/image%20%2818%29.png)

The styling for the sidebar is also changed, but if the sidebar is also available in other pages of the custom modules, it should not be modified in the CSS but in the template file of the theme \(conditional rendering based on current route\).

