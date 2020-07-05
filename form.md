# Form

## Get fid from a file in path

{% embed url="https://drupal.stackexchange.com/questions/50278/get-fid-from-file-path" %}

```php
$filename = 'myfirstpony.png';
$query = new EntityFieldQuery();
$result = $query->entityCondition('entity_type', 'file')
  ->propertyCondition('filename', $filename)
  ->execute();
// if you are guaranteed there is exactly one result, then:
$file_object = reset($result['file']);
$fid = $file_object->fid;
// but beware you might get 0 or many results
```

## save file to private directory

{% embed url="https://www.drupal.org/project/drupal/issues/3011648" %}

```php
  $pdfFileDirectory = 'private://inbound-emails/';
  file_prepare_directory($pdfFileDirectory, FILE_CREATE_DIRECTORY);
```

## Config private file directory

{% embed url="https://www.drupal.org/docs/7/distributions/drupal-commons/installing-drupal-commons/configuring-file-system-settings-after" %}



1. In the admin menu, go to **Configuration &gt; File system**.
2. In the **Private file system path** field, enter a local directory used for private files.

   You should set your files directory to exist outside of the document root for your Drupal Commons installation \(for example, not in `http://[site_URL]/files` or `http://[site_URL]/sites/all/files`\).

   Be sure that Drupal can read from and write to the directory, but that the directory can't be accessed remotely.

3. Click **Save configuration**.

dir: `sites/default/files/private/`

{% embed url="https://drupal.stackexchange.com/questions/277826/site-seems-to-miss-the-private-wrapper-how-can-i-fix-it" %}



## Form theme / class

{% embed url="http://api.tripal.info/api/drupal/drupal-7.x%21includes%21form.inc/function/theme\_form\_element/7.x" %}

## Button style

{% embed url="https://www.drupal.org/project/editor\_button\_link/issues/3051461" %}



