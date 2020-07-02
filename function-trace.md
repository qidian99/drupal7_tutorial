# Function trace

## Upon opening a template

* Navigate to /create-aup

```text
[02-Jul-2020 20:03:54 UTC] --validate_document_permission : isd_helper.module:1338
[02-Jul-2020 20:03:54 UTC] --create_school_init : create_school.module:7
[02-Jul-2020 20:03:54 UTC] --custom_module_init : custom_module.module:82
[02-Jul-2020 20:03:54 UTC] --isd_admin_directory_init : isd_admin_directory.module:6
[02-Jul-2020 20:03:54 UTC] --isd_employee_directory_init : isd_employee_directory.module:5
[02-Jul-2020 20:03:54 UTC] --custom_module_aup_create_doc_with_template : custom_module.module:1011
[02-Jul-2020 20:03:54 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:55 UTC] --validate_document_permission : isd_helper.module:1338
[02-Jul-2020 20:03:55 UTC] --create_school_init : create_school.module:7
[02-Jul-2020 20:03:55 UTC] --custom_module_init : custom_module.module:82
[02-Jul-2020 20:03:55 UTC] --isd_admin_directory_init : isd_admin_directory.module:6
[02-Jul-2020 20:03:55 UTC] --isd_employee_directory_init : isd_employee_directory.module:5
[02-Jul-2020 20:03:55 UTC] --custom_module_create_aup : custom_module.module:1372
[02-Jul-2020 20:03:55 UTC] ++document_forms : document.module:214
[02-Jul-2020 20:03:55 UTC] ++document_types : document.module:234
[02-Jul-2020 20:03:56 UTC] --custom_module_views_query_alter : custom_module.module:2002
[02-Jul-2020 20:03:56 UTC] --create_school_form_alter : create_school.module:278
[02-Jul-2020 20:03:56 UTC] --custom_module_form_alter : custom_module.module:1477
[02-Jul-2020 20:03:56 UTC] --get_user_group : isd_helper.module:821
[02-Jul-2020 20:03:56 UTC] --isd_get_schools : isd_helper.module:488
[02-Jul-2020 20:03:56 UTC] --get_user_group : isd_helper.module:821
[02-Jul-2020 20:03:56 UTC] --get_district_school_admin_id : isd_helper.module:58
[02-Jul-2020 20:03:56 UTC] --get_district_school_admin_id_from_subscription : isd_helper.module:116
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --is_dist_school_admin : isd_helper.module:15
[02-Jul-2020 20:03:56 UTC] --if_user_has_og_role : isd_helper.module:42
[02-Jul-2020 20:03:56 UTC] --og_roles_id_map : isd_helper.module:874
[02-Jul-2020 20:03:56 UTC] --is_admin : isd_helper.module:6
[02-Jul-2020 20:03:56 UTC] --validate_document_permission : isd_helper.module:1338
[02-Jul-2020 20:03:56 UTC] --validate_document_permission : isd_helper.module:1338
[02-Jul-2020 20:03:56 UTC] --document_blocks_block_view : document_blocks.module:136
[02-Jul-2020 20:03:56 UTC] --validate_document_permission : isd_helper.module:1338
[02-Jul-2020 20:03:56 UTC] --validate_document_permission : isd_helper.module:1338
[02-Jul-2020 20:03:56 UTC] --document_blocks_block_view : document_blocks.module:136
[02-Jul-2020 20:03:56 UTC] --aup_create_content_block_callback : document_blocks.module:313
[02-Jul-2020 20:03:56 UTC] --isd_student_directory_block_view : isd_student_directory.module:2336
[02-Jul-2020 20:03:56 UTC] --isd_student_directory_add_file_form : isd_student_directory.module:2356
[02-Jul-2020 20:03:56 UTC] --create_school_form_alter : create_school.module:278
[02-Jul-2020 20:03:56 UTC] --custom_module_form_alter : custom_module.module:1477
[02-Jul-2020 20:03:56 UTC] --isd_admin_directory_add_file_form : isd_admin_directory.module:141
[02-Jul-2020 20:03:56 UTC] --create_school_form_alter : create_school.module:278
[02-Jul-2020 20:03:56 UTC] --custom_module_form_alter : custom_module.module:1477
[02-Jul-2020 20:03:56 UTC] --isd_employee_directory_block_view : isd_employee_directory.module:153
[02-Jul-2020 20:03:56 UTC] --isd_educator_directory_add_file_form : isd_employee_directory.module:180
[02-Jul-2020 20:03:56 UTC] --create_school_form_alter : create_school.module:278
[02-Jul-2020 20:03:56 UTC] --custom_module_form_alter : custom_module.module:1477
[02-Jul-2020 20:03:56 UTC] --isd_employee_directory_block_view : isd_employee_directory.module:153
[02-Jul-2020 20:03:56 UTC] --isd_employee_directory_add_file_form : isd_school_district_employee_directory.inc:1634
[02-Jul-2020 20:03:56 UTC] --create_school_form_alter : create_school.module:278
[02-Jul-2020 20:03:56 UTC] --custom_module_form_alter : custom_module.module:1477
[02-Jul-2020 20:03:56 UTC] --isd_super_admin_directory_add_file_form : isd_super_admin_directory.inc:1065
[02-Jul-2020 20:03:56 UTC] --create_school_form_alter : create_school.module:278
[02-Jul-2020 20:03:56 UTC] --custom_module_form_alter : custom_module.module:1477
[02-Jul-2020 20:03:56 UTC] --validate_document_permission : isd_helper.module:1338
[02-Jul-2020 20:03:56 UTC] --validate_document_permission : isd_helper.module:1338
[02-Jul-2020 20:03:56 UTC] --validate_document_permission : isd_helper.module:1338
[02-Jul-2020 20:03:56 UTC] --custom_module_preprocess_page : custom_module.module:2097
[02-Jul-2020 20:03:56 UTC] --isd_admin_directory_preprocess_page : isd_admin_directory.module:33
[02-Jul-2020 20:03:56 UTC] --isd_employee_directory_preprocess_page : isd_employee_directory.module:80
[02-Jul-2020 20:03:56 UTC] --custom_module_field_group_pre_render_alter : custom_module.module:1782
[02-Jul-2020 20:03:56 UTC] --custom_module_field_group_pre_render_alter : custom_module.module:1782
[02-Jul-2020 20:03:56 UTC] --custom_module_field_group_pre_render_alter : custom_module.module:1782
[02-Jul-2020 20:03:56 UTC] --custom_module_field_group_pre_render_alter : custom_module.module:1782
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:56 UTC] --extract_value : isd_helper.module:981
[02-Jul-2020 20:03:57 UTC] --create_school_init : create_school.module:7
[02-Jul-2020 20:03:57 UTC] --custom_module_init : custom_module.module:82
[02-Jul-2020 20:03:57 UTC] --isd_admin_directory_init : isd_admin_directory.module:6
[02-Jul-2020 20:03:57 UTC] --isd_employee_directory_init : isd_employee_directory.module:5
[02-Jul-2020 20:03:59 UTC] --create_school_init : create_school.module:7
[02-Jul-2020 20:03:59 UTC] --custom_module_init : custom_module.module:82
[02-Jul-2020 20:03:59 UTC] --isd_admin_directory_init : isd_admin_directory.module:6
[02-Jul-2020 20:03:59 UTC] --isd_employee_directory_init : isd_employee_directory.module:5

```

## Menu callbacks

`custom_module.module`

{% code title="custom\_module\_menu\(\)" %}
```php
 $items['aup-create-document-with-template/%'] = array(
    'title' => t('AUP Create document with template'),
    'page callback' => 'custom_module_aup_create_doc_with_template',
    'page arguments' => array(1),
    'access callback' => 'validate_document_permission',
    'access arguments' => array('AUP Create'),
    'type' => MENU_CALLBACK,
  );
```
{% endcode %}

> ### constant MENU\_CALLBACK
>
> Menu type -- A hidden, internal callback, typically used for API calls.
>
> Callbacks simply register a path so that the correct function is fired when the URL is accessed. They do not appear in menus or breadcrumbs.



What comes after this "hidden callback"? Set session specific variables and redirect.

{% code title="custom\_module\_aup\_create\_doc\_with\_template\($nid\)" %}
```php
$template = node_load($nid);
  if(isset($template->nid)) {
    //drupal_set_message('<pre>'. print_r($template, true).'</pre>');
    $_SESSION['aup_document_title'] = $template->title;
    $_SESSION['aup_document_template_id'] = $template->nid;
    $_SESSION['aup_document_content'] = extract_value($template->body, 'value');
    drupal_goto('/create-aup');
  }
```
{% endcode %}

### Define the permission

`isd_helper.module`

{% code title="validate\_document\_permission\($permission = FALSE, $gid = NULL\)" %}
```php
/**
 * Check permissions for Document document type
 */
function validate_document_permission($permission = FALSE, $gid = NULL) {
	error_log("--" . __FUNCTION__ . " : " . basename(__FILE__) . ":" . __LINE__);
	//$caller = get_caller();
	//error_log("Caller:$caller");
	return TRUE;

	if ($permission == FALSE) {
		return FALSE;
	}
	global $user;
	$is_admin = user_has_role(3, $user);
	/**
	 * Allow permission if it is Admin user (iSAFE Admin)
	 */
	/*if($is_admin) {
      return true;
    }*/
	$account = user_load($user->uid);
	$groups = og_get_groups_by_user($account);

	// temp group id
	$gid = @array_values($groups['node'])[0];
	//drupal_set_message($gid);
	//$gid = 1;
	$roles = og_get_user_roles($group_type = 'node', $gid, $account->uid);
	$logged_user_roles = og_get_user_roles($group_type = 'node', $gid, $account->uid);
	$role_permissions = og_role_permissions($roles);
	//$is_member = og_is_member(2, 'user', $account);
	//drupal_set_message('<pre> Is admin user: '. print_r($is_admin, true).'</pre>');
	//drupal_set_message('<pre>'. print_r($role_permissions, true).'</pre>');
	//drupal_set_message('<pre>'. print_r($logged_user_roles, true).'</pre>');
	//drupal_set_message('<pre>'. print_r($is_member, true).'</pre>');
	//drupal_set_message('<pre>'. print_r($groups, true).'</pre>');
	//drupal_set_message('<pre>'. print_r($account, true).'</pre>');
	//drupal_set_message('<pre> gid'. print_r($gid, true).'</pre>');
	$ret = FALSE;
	switch ($permission) {
		case 'AUP Create':
			$if_user_can = og_user_access($group_type = 'node', $gid, $permission, $account) == 1 ? 1 : 0;
			//drupal_set_message('<pre>'. print_r($if_user_can, true).'</pre>');

			if (!$if_user_can) {
				$ret = FALSE;
			}
			else {
				$ret = TRUE;
			}
			// form_set_error('Permission', t('You are not authorized to create AUP.'));


			break;
		case 'AUP Reporting':
			$if_user_can = og_user_access($group_type = 'node', $gid, $permission, $account) == 1 ? 1 : 0;
			//drupal_set_message('<pre>'. print_r($if_user_can, true).'</pre>');

			if (!$if_user_can) {
				$ret = FALSE;
			}
			else {
				$ret = TRUE;
			}
			break;
		case 'SD Import': // import student directory
			$if_user_can = og_user_access($group_type = 'node', $gid, $permission, $account) == 1 ? 1 : 0;
			//drupal_set_message('<pre>'. print_r($if_user_can, true).'</pre>');

			if (!$if_user_can) {
				$ret = FALSE;
			}
			else {
				$ret = TRUE;
			}
			break;

		default:
			$ret = FALSE;
			break;
	}
	return $ret;

}
```
{% endcode %}

### What happened after redirection

```php
  $items['create-aup'] = array(
    'page callback' => 'custom_module_create_aup',
    'access callback' => 'validate_document_permission',
    'access arguments' => array('AUP Create'),
    'type' => MENU_CALLBACK,
  );
```

