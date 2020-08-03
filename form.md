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

## File Type

```php
$import_info['file'] = array(
    '#type' => 'managed_file',
    '#progress_indicator' => 'bar',
    '#upload_validators' => array(
      'file_validate_extensions' => array('csv'),
    ),
    '#title' => t('Choose file'),
    '#title_display' => 'invisible',
    '#size' => 20,
    // '#theme_wrappers' => array(),
  );
```

## Manually start a file download

{% embed url="http://blog.sebcorbin.fr/en/how-force-downloading-file-drupal-7" %}

```php
function mymodule_download_file() {
  if (!isset($_GET['file']) || !file_exists($_GET['file'])) {
    return drupal_not_found();
  }
  $filepath = $_GET['file'];
  $realpath = realpath($path);
  $filename = basename($filepath);
  $extension = pathinfo($filepath, PATHINFO_EXTENSION);
  // Check extension and restrict to files in DRUPAL_ROOT
  if(in_array($extension, array('jpg', 'png', 'gif', 'mp4')) && substr($path, 0, strlen(DRUPAL_ROOT)) === DRUPAL_ROOT) {
    drupal_add_http_header('Content-disposition', 'attachment; filename=' . $filename);
    readfile($filepath);
  }
  else {
    return drupal_access_denied();
  }
}
```

### A php way

{% embed url="https://stackoverflow.com/questions/16251625/how-to-create-and-download-a-csv-file-from-php-script" %}

```php
function array_to_csv_download($array, $filename = "export.csv", $delimiter=";") {
    // open raw memory as file so no temp files needed, you might run out of memory though
    $f = fopen('php://memory', 'w'); 
    // loop over the input array
    foreach ($array as $line) { 
        // generate csv lines from the inner arrays
        fputcsv($f, $line, $delimiter); 
    }
    // reset the file pointer to the start of the file
    fseek($f, 0);
    // tell the browser it's going to be a csv file
    header('Content-Type: application/csv');
    // tell the browser we want to save it instead of displaying it
    header('Content-Disposition: attachment; filename="'.$filename.'";');
    // make php send the generated csv lines to the browser
    fpassthru($f);
}
```

### The problem is tmp file only has file pointer rather than names...

Note that `tmpfile()` returns a file handle, but all the functions you have need a file _path_ \(i.e a string\), not a handle - notably `basename`, `filesize`, and `readfile`. So none of those function calls will work correctly. Also `basename` won't return a file extension either. Just call it whatever you want, i.e

```text
'Content-Disposition: attachment; filename=data.csv'
```

### Another problem is the AJAX request...

{% embed url="https://stackoverflow.com/questions/4545311/download-a-file-by-jquery-ajax" %}

## How to create a multi-step form

In form, switch $form\_state for some value, and assign an id to the form itself

```php
  $form['#id'] = $form_id;
```

In form submit handler,

```php
function YOUR_FORM_submit($form, &$form_state)
{
  switch ($form_state['input']['_triggering_element_value']) {
    case 'Edit': {
        $form_state['mode'] = 'edit';
        break;
      }
    default: {
        $form_state['mode'] = 'view';
      }
  }

  $form_state['rebuild'] = TRUE;
}

```

In form callback handler,

```php

function YOUR_FORM_callback($form, &$form_state)
{
  return $form;
}

```

