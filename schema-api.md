# Schema API

## Add ENUM Type support for MySQL

{% embed url="https://www.drupal.org/project/drupal/issues/1464354" %}

```php
...

 $schema['vchess_games'] = array(
      'description' => 'This table contains a summary of each game',
      'fields' => array(
          'turn' => array(
              'description' => 'Whose turn it is to play, either "w" (white) or "b" (black)',
              'type' => 'enum',
              'enum_items' => array('w', 'b'),
              'not null' => TRUE,
              'default' => 'w',
          ),
       'status' => array(
              'description' => 'Status of the game',
              'type' => 'enum',
              'enum_items' => array('in progress','1/2-1/2','1-0','0-1'),
              'not null' => TRUE,
          ),
...
In the MySQL version of schema.inc in /includes/database/mysql/schema.inc file add code for using these ENUM items:

protected function createFieldSql($name, $spec) {
    $sql = "`" . $name . "` " . $spec['mysql_type'];

    if (in_array($spec['mysql_type'], array('VARCHAR', 'CHAR', 'TINYTEXT', 'MEDIUMTEXT', 'LONGTEXT', 'TEXT')) && isset($spec['length'])) {
      $sql .= '(' . $spec['length'] . ')';
    }
    // New ENUM code begins here:
    elseif ($spec['mysql_type'] == 'ENUM') {
      // Build a string of the enum items like "('a','b','c')"
      $sql .= '(';
      foreach ($spec['enum_items'] as $enum_item) {
        $sql .= "'" . $enum_item . "',";
      }
      $sql = trim($sql, ",");  // Remove the final trailing comma
      $sql .= ')';
    }
    // End of new ENUM code
    elseif (isset($spec['precision']) && isset($spec['scale'])) {
      $sql .= '(' . $spec['precision'] . ', ' . $spec['scale'] . ')';
    }
...
In the same file, add 'enum:normal' => 'ENUM', to the getFieldTypeMap() function:


    public function getFieldTypeMap() {
    // Put :normal last so it gets preserved by array_flip. This makes
    // it much easier for modules (such as schema.module) to map
    // database types back into schema types.
    // $map does not use drupal_static as its value never changes.
    static $map = array(
      'varchar:normal'  => 'VARCHAR',
      'char:normal'     => 'CHAR',

      'text:tiny'       => 'TINYTEXT',
      'text:small'      => 'TINYTEXT',
      'text:medium'     => 'MEDIUMTEXT',
      'text:big'        => 'LONGTEXT',
      'text:normal'     => 'TEXT',

      'serial:tiny'     => 'TINYINT',
      'serial:small'    => 'SMALLINT',
      'serial:medium'   => 'MEDIUMINT',
      'serial:big'      => 'BIGINT',
      'serial:normal'   => 'INT',

      'int:tiny'        => 'TINYINT',
      'int:small'       => 'SMALLINT',
      'int:medium'      => 'MEDIUMINT',
      'int:big'         => 'BIGINT',
      'int:normal'      => 'INT',

      'float:tiny'      => 'FLOAT',
      'float:small'     => 'FLOAT',
      'float:medium'    => 'FLOAT',
      'float:big'       => 'DOUBLE',
      'float:normal'    => 'FLOAT',

      'numeric:normal'  => 'DECIMAL',
        
      'enum:normal'    => 'ENUM',   // This is the line to add for ENUM

      'blob:big'        => 'LONGBLOB',
      'blob:normal'     => 'BLOB',
    );
    return $map;
  }
```



