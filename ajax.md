# Ajax

## Ajax callback

{% embed url="https://www.drupal.org/docs/7/api/javascript-api/simple-drupal-ajax-load-with-jquery-and-delivery-callback" %}

> The real trick here is to get only the HTML you need instead of rendering the header, footer, and every other element that comes with a full page load. This is where the 'delivery callback' setting in [hook\_menu](https://api.drupal.org/api/drupal/modules!system!system.api.php/function/hook_menu/7) comes into play. The 'delivery callback' setting defaults to [drupal\_deliver\_html\_page\(\)](https://api.drupal.org/api/drupal/includes!common.inc/function/drupal_deliver_html_page/7) which returns a fully rendered HTML page. We need to define our own delivery callback function returning just the HTML we want to render via AJAX on the client side.



{% embed url="https://www.drupal.org/docs/7/api/javascript-api/ajax-forms-in-drupal-7" %}

## Onclick conflict

[http://www.maged.me/blog/drupal-7-execute-javascript-code-after-ajax-call](http://www.maged.me/blog/drupal-7-execute-javascript-code-after-ajax-call)







{% embed url="https://www.drupal.org/forum/support/module-development-and-code-questions/2013-09-04/ajax-form-submission" %}





