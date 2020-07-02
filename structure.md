# Structure

## Layout and Navigation

### Where is the theme definition

`/var/www/dev/isddian/sites/all/themes/bootstrap_child`

### Where the menu links records are located?

```sql
SELECT * FROM ISDDIAN.menu_links;
```

![](.gitbook/assets/image%20%2821%29.png)

### How the navigation menu is defined

* Structure \| Menus \| Add Menu
* Structure \| Blocks \| Add Menu block
  * Can start from different levels
  * Will show if the previous level \(up to N-1\) all match the URL

### How image icons are inserted in the BG

{% code title="/sites/all/themes/bootstrap\_child/css/style.css" %}
```css
body .left_vertical_nav ul.menu li a {
  background: url(../images/sprite-icons.png) no-repeat 0 0 transparent;
  text-indent: -5000px;
  outline: none;
  display: block;
  width: 68px;
  height: 68px;
}
body .left_vertical_nav ul.menu li:first-child a {
  background-position: 0 0;
}
body .left_vertical_nav ul.menu li.active-trail:first-child a {
  background-position: -78px 0px;
}
body .left_vertical_nav ul.menu li:nth-child(2) a {
  background-position: 0 -77px;
}
body .left_vertical_nav ul.menu li:nth-child(3) a {
  background-position: 0 -157px;
}
body .left_vertical_nav ul.menu li:nth-child(4) a {
  background-position: 0 -241px;
}
body .left_vertical_nav ul.menu li:nth-child(5) a {
  background-position: 0 -318px;
}
body .left_vertical_nav ul.menu li:nth-child(6) a {
  background-position: 0 -394px;
}
body .left_vertical_nav ul.menu li:nth-child(7) a {
  background-position: 0 -470px;
}
body .left_vertical_nav ul.menu li:nth-child(8) a {
  background-position: 0 -549px;
}
body .left_vertical_nav ul.menu li:nth-child(9) a {
  background-position: 0 -620px;
}
body .left_vertical_nav ul.menu li:nth-child(10) a {
  background-position: 0 -696px;
}
```
{% endcode %}

### Why two Main Menu on the home page

{% code title="/sites/all/themes/bootstrap\_child/templates/system/page.tpl.php" %}
```php
<div class="left_vertical_nav"> <!-- show vertical navigation -->
  <?php if (!empty($primary_nav)): ?>
    <?php print render($primary_nav); ?>
  <?php endif; ?>
</div>
```
{% endcode %}

## Views and Blocks

### How a view gets renders after being defined in the Views UI

1. Type: node -- select from node table
2. Filter -- query conditions 
3. Contextual filter -- supposed select all the AUPs within the school

```javascript

		$('body').on('click', '.template_filter_wrapper .template_filter_inner .grid_view', function () {
			$('#block-views-document-template-listing-block').hide();
			$('#block-views-document-template-grid-block').show();
		});
		$('body').on('click', '.template_filter_wrapper .template_filter_inner .list_view', function () {
			$('#block-views-document-template-listing-block').show();
			$('#block-views-document-template-grid-block').hide();
		});
```

In block: there will be a block called `View: Document Template listing: Document Template listing`

```css
body .view-id-document_template_listing.document-grid-view-block-wrapper .view-content .item-list ul li a {
  display: block;
  border-radius: 25px;
  color: #fff;
  position: relative;
  background: url("../images/sprite-icons.png") no-repeat -744px -461px #3583c5;
  background-size: 870px;
  width: 175px;
  height: 175px;
  padding-top: 113px;
  text-align: center;
  font-size: 18px;
  cursor: pointer;
  text-decoration: none;
  opacity: 0.8;
  -webkit-transition: all 0.2s ease;
  -moz-transition: all 0.2s ease;
  -ms-transition: all 0.2s ease;
  -o-transition: all 0.2s ease;
  transition: all 0.2s ease;
  padding-left: 10px;
  padding-right: 10px;
}
body .view-id-document_template_listing.document-grid-view-block-wrapper .view-content .item-list ul li a:after {
  content: "Open >";
  position: absolute;
  font-size: 14px;
  box-sizing: border-box;
  padding: 10px;
  left: 0;
  width: 100%;
  bottom: 5px;
}
body .view-id-document_template_listing.document-grid-view-block-wrapper .view-content .item-list ul li a:hover {
  opacity: 1;
}
```

### Document Blocks

`/sites/default/modules/document_blocks`

In the function `document_blocks_block_info`, we define the block `aup_sidebar_feature_buttons`

In the function `document_blocks_block_configure` we define the form to add video/text

In the function `document_blocks_block_save` we save the form variables

```php
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
```

{% embed url="https://api.drupal.org/api/drupal/includes%21bootstrap.inc/function/variable\_set/7.x" %}

In the function `document_blocks_block_view`, we set the view for the block \(in this case, a form\)

```php
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

css for the form defined in the bootstrap sub-theme `/sites/all/themes/bootstrap_child/css/style.css`

```css
body.page-edit-aup #block-document-blocks-aup-sidebar-feature-buttons .document_sidebar_feature_box .footer_section .footer_label, body.node-type-aup #block-document-blocks-aup-sidebar-feature-buttons .document_sidebar_feature_box .footer_section .footer_label, body.page-create-aup #block-document-blocks-aup-sidebar-feature-buttons .document_sidebar_feature_box .footer_section .footer_label {
  color: #fff;
  margin-bottom: 7px;
}
```

## Crucial different for using theme in render array and in theme function

```php
$content = array(
  '#theme' => 'statistics_component',
  '#bars' => $bars,
  '#last' => $last,
  '#overall' => $overall,
  '#attached' => array(
    'css' => array(
      drupal_get_path('module', 'aup_mock') . '/css/aup-statistics.css',
    ),
  ),
);
```

All the variables are the final ones!



1. [template\_preprocess Drupal 7](http://api.drupal.org/api/function/template_preprocess/7) This is always added by core. The [variables generated here](https://www.drupal.org/node/226776) are used for every templated hook.
2. template\_preprocess\__hook_ This is supplied by a module or core file that implements a theming hook. The initial generation of all the variables specific to this hook is usually done here.
3. _moduleName_\_preprocess Do not confuse this with the preprocessor before it. This allows modules that did not originally implement the hook to influence the variables. Applies to all hooks.
4. _moduleName_\_preprocess\__hook_ Same idea as the previous preprocessor but for specific hooks.
5. _engineName_\_engine\_preprocess _- The preprocessor for theming engines. Applies to all hooks._
6. _engineName_\_engine\_preprocess\__hook_ Another preprocessor for theming engines but specific to a single hook.
7. _engineName_\_preprocess NOT RECOMMENDED. This is the first preprocessor that can be used inside the theme. It can be named after the theme engine the theme is running under. Applies to all hooks.
8. _engineName_\_preprocess\__hook_ NOT RECOMMENDED. Another preprocessor named after the engine but specific to a single hook.
9. _themeName_\_preprocess This one is named after the theme itself. Applies to all hooks.
10. _themeName_\_preprocess\__hook_ Same as the previous preprocessor but for a specific hook.



Preferred way:

```php
'description-component' => array(
  '#markup' => theme('description_component'),
  '#attached' => array(
    'css' => array(
      drupal_get_path('module', 'aup_mock') . '/css/aup-description.css',
    ),
  ),
),
```

