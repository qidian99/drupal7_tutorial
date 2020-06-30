# Structure



## Why two Main Menu on the home page

{% code title="/sites/all/themes/bootstrap\_child/templates/system/page.tpl.php" %}
```php
<div class="left_vertical_nav"> <!-- show vertical navigation -->
  <?php if (!empty($primary_nav)): ?>
    <?php print render($primary_nav); ?>
  <?php endif; ?>
</div>
```
{% endcode %}

