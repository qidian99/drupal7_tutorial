# Use Drupal to build custom module that affords CRUD operations

## UI Prototype

{% embed url="https://www.figma.com/proto/EiuDQUYlZCc4n11mf7Rmrw/Drupal-CRUD-API?node-id=1%3A98&scaling=min-zoom" %}

### Schools

![](../../.gitbook/assets/image%20%2815%29.png)

### School

![](../../.gitbook/assets/image%20%2812%29.png)

### Create School

![](../../.gitbook/assets/image%20%285%29.png)

### Edit School

![](../../.gitbook/assets/image%20%284%29.png)

### Delete School

Any delete button

## Drupal Modules

NOTE: Actually not all modules listed below are used.

* Install Drupal 7 from **Acquia Desktop** \(drupal\_7\_72\)

{% embed url="https://dev.acquia.com/downloads" %}

* Form-API
* Entity-API
* Views
  * For filtering the nodes based on content-type
* Devel
  * For development utilities
* Pathauto
  * For renaming the path following REST-ful guidelines

If using `drush`,  do the following commands

```text
drush en views devel pathauto -y
```

## Basic Implementation

### Schools module and fetch all schools

{% page-ref page="create-the-schools-module.md" %}

{% embed url="https://www.folio3.com/how-to-create-a-custom-module-in-drupal-7" caption="Reference" %}

### Page for individual schools

{% page-ref page="create-individual-school-page.md" %}

### Forms for insertion, update, and deletion

{% page-ref page="create-form-1.md" %}

## Styling

### Show form in modal popup

{% page-ref page="show-form-in-modal-popup.md" %}

### Customize form css

{% page-ref page="customize-form-css.md" %}

### Create a block for school form

{% page-ref page="create-a-block-for-school-forms.md" %}



