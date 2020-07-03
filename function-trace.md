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

## create AUP function

### form

```php
$type='aup';
  $node = (object) array(
    'uid' => $user->uid,
    'name' => isset($user->name) ? $user->name : '',
    'type' => $type,
    'language' => LANGUAGE_NONE,
  );

  $form = node_add($type);
```

{% code title="document\_blocks.module" %}
```php
// aup_sidebar_feature_buttons


case 'aup_sidebar_feature_buttons':
      $aup_sidebar_feature_buttons = variable_get('aup_sidebar_feature_buttons', array(
        'aup_head_logo_text' => '',
        'aup_head_text_box' => '',
        'aup_add_video' => '',
        'aup_add_seal' => '',
        'aup_add_questions' => '',
        'aup_add_text' => '',
        'aup_add_footer' => '',
        'aup_add_legal_text' => '',

      ));
      $content = '';
      $content .= '<div class="document_sidebar_feature_box">';
        $content .= '<div class="header_section">';

          $content .= '<div class="box_title black_title">Header</div>';
          $content .= '<div class="box aup_head_logo_slogan_button">';
            $content .= '<div class="box_head"><span class="left">' . $aup_sidebar_feature_buttons['aup_head_logo_text'] .'</span><span class="right">'.$aup_sidebar_feature_buttons['aup_head_text_box'].'</span></div>';
            $content .= '<div class="box_body">&nbsp;</div>';
          $content .= '</div>';
        $content .= '</div>';


        $content .= '<div class="content_section">';

          $content .= '<div class="box_title black_title">Content</div>';
          $content .= '<div class="box aup_content_add_video_button">';
            $content .= '<div class="box_head"><span>&nbsp;</span></div>';
            $content .= '<div class="box_body">' . $aup_sidebar_feature_buttons['aup_add_video'] .'</div>';
          $content .= '</div>';
          $content .= '<div class="box">';
            $content .= '<div class="box_head"><span>&nbsp;</span></div>';
            $content .= '<div class="box_body">' . $aup_sidebar_feature_buttons['aup_add_seal'] .'</div>';
          $content .= '</div>';
          $content .= '<div class="box aup_content_add_questions">';
            $content .= '<div class="box_head"><span>&nbsp;</span></div>';
            $content .= '<div class="box_body">' . $aup_sidebar_feature_buttons['aup_add_questions'] .'</div>';
          $content .= '</div>';
          $content .= '<div class="box aup_content_add_text">';
            $content .= '<div class="box_head"><span>&nbsp;</span></div>';
            $content .= '<div class="box_body">' . $aup_sidebar_feature_buttons['aup_add_text'] .'</div>';
          $content .= '</div>';
        $content .= '</div>';

        $content .= '<div class="footer_section">';

          $content .= '<div class="box_title white_title">Footer</div>';
          $content .= '<div class="box">';
            $content .='<div class="footer_label">' . $aup_sidebar_feature_buttons['aup_add_footer'] .'</div>';
            $content .= '<div class="box_head"><span>&nbsp;</span></div>';
            $content .= '<div class="box_body">&nbsp;</div>';
          $content .= '</div>';
          $content .= '<div class="box">';
            $content .='<div class="footer_label">' . $aup_sidebar_feature_buttons['aup_add_legal_text'] .'</div>';
            $content .= '<div class="box_head"><span>&nbsp;</span></div>';
            $content .= '<div class="box_body">&nbsp;</div>';
          $content .= '</div>';

        $content .= '</div>';

      $content .= '</div>';

      $block['content'] = $content;

      break;
```
{% endcode %}

### document\_block

left side bar: options to add to AUP

```php
/**
 * Implements hook_block_save().
 */
function document_blocks_block_save($delta = '', $edit = array())

{
  error_log("--" . __FUNCTION__ . " : " . basename(__FILE__) . ":" . __LINE__);
  switch ($delta) {
    case 'aup_sidebar_feature_buttons':
      variable_set('aup_sidebar_feature_buttons', array(
        'aup_head_logo_text' => $edit['aup_head_logo_text'],
        'aup_head_text_box' => $edit['aup_head_text_box'],
        'aup_head_text_box' => $edit['aup_head_text_box'],
        'aup_add_video' => $edit['aup_add_video'],
        'aup_add_seal' => $edit['aup_add_seal'],
        'aup_add_questions' => $edit['aup_add_questions'],
        'aup_add_text' => $edit['aup_add_text'],
        'aup_add_footer' => $edit['aup_add_footer'],
        'aup_add_legal_text' => $edit['aup_add_legal_text'],
      ));

      break;
  }
}    

```

content: AUP content

{% code title="aup\_create\_content\_block.tpl.php" %}
```text
<?php

/**
 * @file
 * Default theme implementation to display a block.
 *
 * Available variables:
 * - $block->subject: Block title.
 * - $content: Block content.
 * - $block->module: Module that generated the block.
 * - $block->delta: An ID for the block, unique within each module.
 * - $block->region: The block region embedding the current block.
 * - $classes: String of classes that can be used to style contextually through
 *   CSS. It can be manipulated through the variable $classes_array from
 *   preprocess functions. The default values can be one or more of the
 *   following:
 *   - block: The current template type, i.e., "theming hook".
 *   - block-[module]: The module generating the block. For example, the user
 *     module is responsible for handling the default user navigation block. In
 *     that case the class would be 'block-user'.
 * - $title_prefix (array): An array containing additional output populated by
 *   modules, intended to be displayed in front of the main title tag that
 *   appears in the template.
 * - $title_suffix (array): An array containing additional output populated by
 *   modules, intended to be displayed after the main title tag that appears in
 *   the template.
 *
 * Helper variables:
 * - $classes_array: Array of html class attribute values. It is flattened
 *   into a string within the variable $classes.
 * - $block_zebra: Outputs 'odd' and 'even' dependent on each block region.
 * - $zebra: Same output as $block_zebra but independent of any block region.
 * - $block_id: Counter dependent on each block region.
 * - $id: Same output as $block_id but independent of any block region.
 * - $is_front: Flags true when presented in the front page.
 * - $logged_in: Flags true when the current user is a logged-in member.
 * - $is_admin: Flags true when the current user is an administrator.
 * - $block_html_id: A valid HTML ID and guaranteed unique.
 *
 * @see bootstrap_preprocess_block()
 * @see template_preprocess()
 * @see template_preprocess_block()
 * @see bootstrap_process_block()
 * @see template_process()
 *
 * @ingroup templates
 */
/**
 * @var $vars : This will provide all the values from hook_block_view().
 */
$files_url = variable_get('file_' . file_default_scheme() . '_path', conf_path() . '/files/images');
$nid =  arg(1);
$node = '';
if(is_numeric($nid)) {
  $node = node_load($nid);
}
/*echo '<pre>';
print_r($node);
echo '</pre>';*/

if (isset($node->title) && !empty($node->title)){
  $title = $node->title;
} else if(isset($_SESSION['aup_document_title']) && !empty($_SESSION['aup_document_title'])) {
  $title = $_SESSION['aup_document_title'];
} else {
  $title = 'Acceptable Use Policy Agrerments';
}
?>

<div class="document_main_wrapper">
  <div class="header_initial_title_section">
    <div class="doc_title_edit_button_wrapper document_edit_section">
      <div class="doc_title_update_button"></div>
    </div>
    <div class="documnt_title">
      <?php echo $title; ?>
    </div>
  </div>
  <div class="document_header_section">
    <?php
    // buttons comes from @custom_module
    /*$if_preview = arg(0);
    $nid = arg(1);
    if($if_preview == 'aup-campaign' && is_numeric($nid)): */?><!--
      <div class="document_preview_buttons">
        <a class="action-button-user blue_button button" href="<?php /*print '/edit-aup/' . $nid */?>">Back</a>
        <a class="action-button-user blue_button button disabled_btn" href="#">Save</a>
        <a class="action-button-user blue_button button disabled_btn" href="#">Save & Test </a>
        <a class="action_button_send blue_button button" href="#">Send</a>
      </div>
    --><?php /*endif;*/
    $image_url = '';
    $file_id = 0;
    if(isset($node->field_document_logo['und'][0]['fid'])):
      $file_id = $node->field_document_logo['und'][0]['fid'];
    elseif(isset($node->field_document_logo_source['und'][0]['value'])):
      $image_url = $node->field_document_logo_source['und'][0]['value'];
    endif;
    $text = '';
    if(isset($node->field_document_slogan['und'][0]['value'])):
      $text = $node->field_document_slogan['und'][0]['value'];
    endif;
    if($file_id == 0 && empty($image_url) && empty($text)):

    ?>

    <?php endif; ?>
    <div class="header_edit_section <?php print ($file_id == 0 && empty($image_url) && empty($text) ) ? 'hide_me' : '' ?>">
      <div class="doc_logo_section">
        <div class="doc_logo edit_hover">
          <div class="doc_logo_edit edit_button document_edit_section"><span></span></div>
          <?php if($file_id == 0 && empty($image_url) && !empty($node)): ?>
            <span class="temp_text">LOGO</span>
            <img src="" class="hide_me"/>
          <?php elseif($file_id > 0):
              $output = field_view_field('node', $node, 'field_document_logo');
              print render($output);
            elseif(!empty($image_url)): ?>
              <img src="<?php print $image_url ?>" />
            <?php else: ?>
                <img src="" class="hide_me"/>
            <?php endif; ?>
          <?php
           ?>
        </div>

      </div>
      <div class="doc_slogan_section">
        <div class="doc_slogan edit_hover">
          <div class="doc_slogan_edit edit_button document_edit_section"><span></span></div>
          <span class="temp_text">
            <?php
              $text = (empty($text)) ? 'TEXT' : $text;
              print $text;
            ?>
          </span>
        </div>
      </div>
    </div>
  </div>
  <div class="document_content_section">
    <div class="document_content_wrapper">
      <div class="docuument_text_edit_button_wrapper document_edit_section">
        <div class="document_text_update_button"></div>
      </div>
      <?php
      $text = '';
      if(isset($node->body['und'][0]['value'])):
        $text = $node->body['und'][0]['value'];
      elseif(isset($_SESSION['aup_document_content']) && !empty($_SESSION['aup_document_content'])):
        $text = $_SESSION['aup_document_content'];
      endif;
      ?>
      <div class="document_body">
        <?php print $text; ?>

      </div>
    </div>
    <!--<img class="demo_image"
         src="/<?php /*echo $files_url . '/aup-content-img.jpg' */?>"/>-->

    <div class="document_add_text_wrap <?php print (empty($node)) ? 'hide_me' : '' ?>">
      <div class="text_edit_button_wrapper document_edit_section">
        <div class="text_update_button"></div>
      </div>
      <?php
      $text = '';
      if(isset($node->field_doc_text_for_parents['und'][0]['value'])):
        $text = $node->field_doc_text_for_parents['und'][0]['value'];
      endif;
      ?>
      <?php if(empty($node) && empty($text)): ?>
        <div class="text_add_button">
          <div class="text_edit_button edit_button"><span></span></div>
          <span class="text">Add Text</span>
        </div>
      <?php endif; ?>

      <div class="document_text_body"><?php print $text; ?></div>

    </div>
    <?php
      $video_url = '';

      if(isset($node->field_video_ref_to_aup['und'][0]['target_id'])):
        $video_node = node_load($node->field_video_ref_to_aup['und'][0]['target_id']);
        if(isset($video_node->field_video_id['und'][0]['value'])):
          $vid = $video_node->field_video_id['und'][0]['value'];
          $video_url = get_video_embed_url_from_id($vid, 'vimeo');
        endif;
      elseif(isset($node->field_document_video_source['und'][0]['value'])):
        $url = $node->field_document_video_source['und'][0]['value'];
        $video_url = get_video_embed_url($url);

      endif;
      //echo 'here...';
    ?>
      <div class="video_section_wrap <?php print (empty($video_url) ? 'hide_me' : '')?>">
        <div class="video_edit_button_wrapper document_edit_section">
          <div class="video_update_button"></div>
        </div>
        <?php if(empty($video_url)): ?>
          <div class="video_add_button document_edit_section">
            <div class="video_edit_button edit_button"><span></span></div>
            <span class="text">Add Video</span>
            <div class="video_icon"></div>
          </div>
        <?php endif; ?>
        <div class="video_player_wrapper">
          <iframe width="100%" height="360" src="<?php print $video_url ?>" frameborder="0" allowfullscreen></iframe>
        </div>
      </div>

    <?php if(isset($node->field_doc_ques_serialize_array['und'][0]['value'])): ?>
      <div class="question_section_wrap">
        <div class="question_edit_button_wrapper document_edit_section">
          <div class="question_update_button"></div>
        </div>
        <div class="demo_questions_listing_view">
          <div class="demo_questions_heading">QUESTIONS</div>
          <div class="demo_questions_body">
            <?php $questions = strval($node->field_doc_ques_serialize_array['und'][0]['value']);

            if(!empty($questions)):
              $questions = unserialize($questions);
              if(is_array($questions) && count($questions)> 0):
                foreach ($questions as $k => $question):
                  /*echo '<pre>';
                    print_r($question);
                  echo '</pre>';*/
                  if(!empty($question['question']['value'])):
                    //echo 'inside';
                    $no = ($k+1);
                    ?>
                    <div class="question_wrapper">
                      <div class="question"><?php print $no; ?>. <?php print $question['question']['value']; ?></div>
                      <div class="question_options" data-id="option_1_1">
                        <?php if(is_array($question['options']) && count($question['options']) > 0): ?>
                          <?php foreach($question['options'] as $o => $option):
                            if(!empty($option['value'])): ?>
                              <div class="question_option_wrapper">
                                <label><input type="radio" name="<?php print $option['key'] ?>" <?php print $question['answer']['value'] == $option['key'] ? 'checked="checked"': ''; ?> value="option_1_1" disabled="disabled"> <?php print $option['value'] ?></label>
                              </div>
                            <?php
                            endif;
                          endforeach; ?>
                        <?php endif; ?>
                      </div>
                    </div>
                  <?php
                  endif;
                endforeach;
              endif;
            endif;
            ?>

          </div>
        </div>
      </div>
    <?php else: ?>
      <div class="question_section_wrap hide_me">
        <div class="question_edit_button_wrapper">
          <div class="question_update_button"></div>
        </div>
        <div class="question_add_button">
          <div class="question_edit_button edit_button"><span></span></div>
          <span class="text">Add Questions</span>

        </div>
        <div class="demo_questions_listing_view hide_me">
          <div class="demo_questions_heading">QUESTIONS</div>
          <div class="demo_questions_body"></div>
        </div>
      </div>
    <?php endif; ?>
    <!-- test video players -->
    <!--<div id="video_player1"></div>-->
    <!--        <div id="spherical-video-player"></div>-->


  </div>
  <div class="document_footer_section">

  </div>
</div>

```
{% endcode %}

