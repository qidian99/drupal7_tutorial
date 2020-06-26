# Create the Schools module

## Create the module directory

Create the directory `DRUPAL_ROOT/sites/all/modules/custom/school`, which includes the following files

* `schools.info` 
  * Drupal uses .info files to store metadata about themes and modules.

    For modules, the .info file is used for:

    * rendering information on the Drupal Web GUI administration pages;
    * providing criteria to control module activation and deactivation;
    * notifying Drupal about the existence of a module;
    * specifying the module's dependencies on other Drupal projects
    * general administrative purposes in other contexts.

    This .info file is required for the system to recognize the presence of a module.  
* `schools.install` 
  * In Drupal 7, .install files can define new tables, load data, and implement conversions during updates.

    A `.install` file is run the first time a module is enabled, and is used to run setup procedures as required by the module. The most common task is creating database tables and fields. The `.install` file does not have any special syntax. It is merely a PHP file with a different extension.

    `.install` files are also used to perform updates when a new version of a module needs it.

  * Let Drupal's **Schema API** to help maintain the table
  * Will explore how to use it update the schema of a table later
* `schools.module`
  * Modules are created to do all sorts of things: create blocks \(abbreviated content that often appears on the right or left side of multiple pages\), create special content types \(for full page content - such as the content you are reading right now\), track back-end information, and more.
  * Different **hooks**
    * For blocks, there are 8 lightweight hooks
      * `hook_block_info():` tells Drupal what block\(s\) your module creates
* `schools.theme.inc`
  * All the templates and style definitions/hooks

## Write the module .info file

`schools.info`

```text
name = Schools
description = "Provides CRUD operations for school data"
core = 7.x
configure = admin/config/content/school
```

## Write the module .install file

`schools.install`

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

## Write the module .theme.inc file

`schools.theme.inc`

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
  return $themes;
}
```

## Write the .module file

`schools.module`

```php
<?php

require_once("schools.theme.inc"); // at the top of schools.module

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
    'title'             =>  'Schools View',  //page title
    'description'       =>  'Schools Information',  //description show when mouse hover on link
    'page callback'     =>  'schools_list',  //callback function which is invoked when menu item is called.
    'access callback'   =>  true,  //any user can access this page
  );
  return $items;
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

```

## Write the .tpl.php file

`schools-list.tpl.php` under `DRUPAL_ROOT/sites/all/themes/bartik/templates/schools/` 

```php
<?php
if ($data->rowCount() > 0) {
  echo "<table><tr><th>Id</th><th>Name</th><th>Address</th><th>Zip Code</th></tr>";
  foreach ($data as $v) {
    echo "<tr>";
    echo "<td>" . $v->sid . "</td>";
    echo "<td>" . $v->name . "</td>";
    echo "<td>" . $v->address . "</td>";
    echo "<td>" . $v->zip_code . "</td>";
    echo "</tr>";
  }
  echo "</table>";
} else {
  echo "No records found";
}

```

## Enable the module

1. Go to _**Modules**_, click the checkbox to enable _**Schools**_, and save your configuration. 
2. To enable the themes flush the caches, go to **Configuration -- Development -- Performance -- CLEAR CACHE**
3. **Important**: Before writing new partial code in the module, make sure to disable the module and save

## Result 01

Go to [http://drupal-7-72.dd:8083/schools](http://drupal-7-72.dd:8083/schools), it should show

![](../../.gitbook/assets/image%20%2811%29.png)

since we don't have any record in the database yet.

## Create stored procedure to inject schools

Open MySQL workbench and connect to `127.0.0.1:33067` using credential `root:YES` 

Check that the table `schools` exists in the database by running

```sql
SELECT * FROM drupal_7_72.schools;
```

![Query result 01](../../.gitbook/assets/image%20%286%29.png)

Now, create the stored procedure

```sql
use drupal_7_72;

DELIMITER $$
DROP PROCEDURE IF EXISTS test$$

CREATE PROCEDURE test()
BEGIN
   DECLARE count INT DEFAULT 0;
   WHILE count < 10 DO
      /**Sql statement**/
      SET count = count + 1;
      INSERT INTO drupal_7_72.schools (name, address, zip_code) 
      VALUES (CONCAT("School ", count), 
			        CONCAT("Address ", count), 
              CONCAT("0000", count));
   END WHILE;
END$$
DELIMITER ;  

SHOW CREATE PROCEDURE test;
call test();
```

After calling the procedure, re-execute the query

```sql
SELECT * FROM drupal_7_72.schools;
```

will give the result

![](../../.gitbook/assets/image%20%282%29.png)

`sid` field will differ since it is defined as serial

Note that the last zip code is invalid, which indicates backend validation is also important.

## Result 02

Go to [http://drupal-7-72.dd:8083/schools](http://drupal-7-72.dd:8083/schools), it should show

![](../../.gitbook/assets/image%20%2814%29.png)

