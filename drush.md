# Drush

## Dummy users

{% embed url="https://drushcommands.com/drush-7x/devel-generate/generate-users/" %}

## Set up connection to Drupal db

In `sites/default/settings.php`

```php
$databases = array (
  'default' =>
  array (
    'default' =>
    array (
      'database' => 'vbo',
      'username' => 'root',
      'password' => '',
      'host' => '127.0.0.1',
      'port' => '33067',
      'driver' => 'mysql',
      'prefix' => '',
    ),
  ),
);

```

