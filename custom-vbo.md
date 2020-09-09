# Custom VBO

## Diagram

![](.gitbook/assets/group-creation-vbo-student.png)

## Details

1. When all\_row is set, we need to store the exposed filters in session

   views-bulk-operations/multipage/selection-update page callback isd\_vbo\_update\_selection\_ajax

   The $\_POST\['item\_ids'\] is 

   ```php
   Array
   (
       [all_rows] => 1
   )
   ```

   We need to only update the current exposed filters to 1, which will be later joined by OR condition in query

2. However, the view object is not preserved in this endpoint
   1. ctools object cache API drupal 7
   2. [https://api.drupal.org/api/ctools/includes%21object-cache.inc/function/ctools\_object\_cache\_get/7.x-1.x](https://api.drupal.org/api/ctools/includes%21object-cache.inc/function/ctools_object_cache_get/7.x-1.x)
   3.   ```text
      function ctools_object_cache_set($obj, $name, $cache, $sid = NULL) {
      ```



Where can we access the view object? `isd_vbo_views_bulk_operations_form_alter`

How can we map the exposed filters? in the hash function `isd_vbo_get_selection_id` `isd_vbo_get_normalized_exposed_filters`

Used ctools to store the options and filters, but the filters is hashed.

Need a reverse mapping from hashed id to filters

Hashing:

```php
foreach ($view->filter as $name => $filter) {
  // dpm($name);
  // dpm($filter);
  if ($filter->is_exposed()) {
    $exposed_filters[$filter->options['expose']['identifier']] = $name;
  }
}
 // Normalize the exposed filter values.
$exposed_input = array_intersect_key($view->get_exposed_input(), $exposed_filters);
$exposed_input = array_filter($exposed_input, function ($value) {
  return $value !== 'All';
});
ksort($exposed_input);f

```



