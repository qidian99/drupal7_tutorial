# Drush

## Dummy users

{% embed url="https://drushcommands.com/drush-7x/devel-generate/generate-users/" %}

## Set up connection to Drupal db

In `sites/default/settings.php`

```php
$databases = array (
  'default' =>
  array (
    'default' =>
    array (
      'database' => 'vbo',
      'username' => 'root',
      'password' => '',
      'host' => '127.0.0.1',
      'port' => '33067',
      'driver' => 'mysql',
      'prefix' => '',
    ),
  ),
);

```

## Install update

{% embed url="https://www.drupal.org/docs/updating-drupal/updating-drupal-core-via-drush" %}



1. Backup both your files and database. Using Drush, type in and execute this command.

   ```text
   drush archive-dump
   ```

   Notes:

   * It is **important** to create backups before updating. So that if something unexpected shows up during or after the update you will be able to quickly and easily revert the update.
   * This _"drush archive-dump"_ command above creates a _.tar.gz_ of files and the database. This is a legacy Drush command. Which is slated for removal in Drush. This command only covers files located under /web directory.

2. Check for available updates  


   ```text
   drush pm-updatestatus
   ```

   * Note: The alias for the command `ups`
   * Note: This command is deprecated for composer based installation, please use `composer-show`

3. Activate [maintenance mode](https://www.drupal.org/node/2827362/)  


   ```text
   drush state-set system.maintenance_mode 1
   ```

   Note: The alias for the command is `sset`

4. Clear the cache  


   ```text
   drush cache-rebuild
   ```

   Notes:

   * The alias for the command is `cr`
   * This command clears the _cache\_\*_ bins in the Drupal database, and then rebuild the site's container

5. Choose one or more options below to execute the updates. Which option\(s\) you choose depends on what type of update\(s\) are needed. `pm-update` \(alias: `up`\) both updates the code as well as apply any pending database updates, the same as `pm-updatecode` + `updatedb`.
   * **Option:** Update Drupal core  


     ```text
     drush pm-update drupal
     ```

   * **Option:** Update Drupal core to a development branch, _for testing and patch creation only \(not Production\)_  


     ```text
     drush pm-update drupal-8.5.x-dev
     ```

   * **Option:** Update a single module  


     ```text
     drush pm-update module_name
     ```

   * **Option:** Update only security updates  


     ```text
     drush pm-update --security-only
     ```
6. If appropriate, re-apply any manual modifications to files such as _.htaccess_, _composer.json_, or _robots.txt_. Drush does not do this automatically.
7. Reapply any core patches you were using before the upgrade \(assuming that these haven't been merged yet\).
   1. These are easy to find with good commit messages.
      * `% git log --oneline --reverse core`
      * `ee2bf8dd Issue #18: Updated Drupal core from 8.3.4 to 8.3.5.`
      * `267e3ad0 Issue #27: Applied patch from https://www.drupal.org/project/drupal/issues/2174633#comment-12291691.`
      * `718ecba5 Issue #9: Applied patch from https://www.drupal.org/project/drupal/issues/2906229#comment-12496488.`
   2. For each previously applied patch since the last core update, use the [git cherry-pick](https://git-scm.com/docs/git-cherry-pick) command \(or fix conflicts if it fails\) in chronological order.
      * `% git cherry-pick 267e3ad0`
      * `% git cherry-pick 718ecba5`
      * `...`
8. **If using Composer to manage PHP libraries** \(e.g. because some contributed modules require it\), update your _/vendor_ directory with the following command:
   * `composer update drupal/core --with-dependencies`
9. Update database, if any required database updates are needed  


   ```text
   drush updatedb
   ```

   Note: The alias for the command is `updb`.

10. Check that your site is ok. To do so:
    1. Using Drupal, look at the status report page
    2. Using a browser test your site by visiting important pages
11. Deactivate maintenance mode  


    ```text
    drush state-set system.maintenance_mode 0
    ```

12. Clear the cache again  


    ```text
    drush cache-rebuild
    ```

13. Done. You have successfully updated your Drupal using Drush :\)

