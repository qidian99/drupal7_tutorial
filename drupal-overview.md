# Drupal Concepts

{% embed url="https://www.drupal.org/docs/7/understanding-drupal/overview" %}

{% embed url="https://www.drupal.org/docs/7/understanding-drupal/general-concepts" %}

{% embed url="https://www.drupal.org/docs/7/theming/overview-of-theme-files" %}

### Overview

![](.gitbook/assets/image%20%2813%29.png)

1. At the base of the system is the collection of nodes—the data pool. Before anything can be displayed on the site, it must be an input as data.
2. The next layer up is where modules live. Modules are **functional plugins** that are either part of the Drupal core \(they ship with Drupal\) or they are contributed items that have been created by members of the Drupal community. Modules build on Drupal's core functionality, **allowing you to customize the data items \(fields\) on your node types**; set up e-commerce; programmatically sorting and display of content \(custom output controlled by filters you define\); and more. There are thousands of different options within the fast-growing [repository of contributed Drupal modules](https://drupal.org/project/modules). They represent the innovation and collaborative effort of everyone from individuals to large corporations.
3. At the next layer, we find blocks and menus. **Blocks often provide the output from a module or can be created to display whatever you want**, and **then can be placed in various spots \(Regions\)** in your **template \(theme\)** layout. Blocks can be configured to output in various ways, as well as only showing on certain defined pages, or only for certain defined users. **Menus** are navigators in Drupal, which define the content coming on each defined menu path \(relative URL\). Menus are a core element of Drupal which provide links to all the pages created in Drupal.
4. Next are user permissions. Permissions determine what users are allowed to do and see. Permissions are assigned \(or not\) to various "roles", which are in turn given to users.  
5. On the top layer is the site theme \(the "skin"\). This is made up predominantly of XHTML and CSS, with some PHP variables intermixed, so Drupal-generated content can go in the appropriate spots. Also included with each theme is a set of functions that can be used to override standard functions in the modules in order to provide complete control over how the modules generate their markup at output time. Templates can also be assigned on-the-fly based on user permissions.

### Node

Essentially, a node is a set of related bits of information. When you create a new blog post, you are not only defining its body text, but also its title, content, author link, creation date, taxonomy \(tags\), etc. Some of these elements will be shown by the theme layer when the node is displayed. Others are meta-data that control when the node will show up at all - such as taxonomy or publishing status.

### Entity type

Entity types are used to store and display data, which can be nodes \(content\), comments, taxonomy terms, user profiles or something custom developed.

### Taxonomy

Drupal has a system for classifying content known as _taxonomy_. This is provided by the core Taxonomy module. You can define your own _vocabularies_ \(groups of _taxonomy terms_\) and add terms to each vocabulary. Each vocabulary can then be attached to one or more content types, and in this way, nodes on your site can be grouped into categories, tagged, or classified in any way you choose

### Module

* **Core** modules are those included with the main download of Drupal. These can be turned on or off without downloading additional components. Examples include _Blog, Book, Poll_, or _Taxonomy_.
* **Contributed** modules are downloaded from the Modules download section of drupal.org, and installed within your Drupal installation. Examples include _Panels, Views_ or _Metatag_.
* **Custom** modules are modules you write yourself. This requires a thorough understanding of Drupal, PHP programming, and Drupal's API.

### Regions

Pages on your Drupal site are laid out in _Regions_. These can include the header, footer, sidebars, featured top, featured bottom, main content regions etc... Your theme may define additional regions.

### Blocks

_Blocks_ are discrete chunks of information that are displayed in the regions of your site's pages. Blocks can take the form of static chunks of HTML or text, menus \(which are for site navigation\), the output from modules \(e.g. hot forum topics\), or dynamic listings that you've created yourself \(e.g. a list of upcoming events\).

### Theme

The _Theme layer_ is separate from the data layer, the functionality extension layer \(module\) and Core. Theme controls the appearance \(look and feel\) of your site, or how your site is displayed, including the graphic look, layout, and colors. A theme consists of one or more PHP template files that define the HTML output of your site's pages, along with one or more CSS files that define the layout, fonts, colors, and other styles.

### Views

Although not all sites have Views, most sites include the Views module because of the excellent tools it provides. Views allows people to **choose a list of nodes or other entities and present them as pages, blocks, RSS feeds, or other formats**. The main use case for views is to create dynamically updating lists of content \(for example, a listing of latest news\), based on properties of that content \(in the case of the news listing, _that the content type is “News” and sorted by publication date_\).

### Views Layout

Views can be created as a page or blocks. View's data can be themed by creating custom templates. Templates can be created to display output, style output and field content. In display output, the user can override the default order of views content structure. In Styled output user can theme the entire HTML structure of view content and for field output for customizing field data.

### Database

Drupal stores information in a database. Within this database, each type of information has its own database table. For example, the basic information about the nodes of your site are stored in the Node table, and each field stores its data in a separate table \(which Drupal creates automatically\). Comments and Users also have their own database tables, as do roles, permissions, and other settings.

### Path

When you visit a path in your Drupal site, Drupal figures out what information should be sent to your browser by checking its list of menu items and routes. Generally, Drupal allows each module to define paths that the module will be responsible for, and when you choose to visit a particular path Drupal asks the module what should be displayed on the page.

For example, the page you are now viewing is [http://drupal.org/node/19828](http://drupal.org/node/19828) - the path is "node/19828". The module that is responsible for this path is the core Node module, so when you visit this page, Drupal lets the Node module determine what to display.



