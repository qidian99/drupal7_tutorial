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

## D8 Install update

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

## D7 Install update

{% embed url="https://www.drupal.org/docs/7/update/updating-drupal-using-drush" %}



#### 1. Backup everything <a id="s-1-backup-everything"></a>

Drush backs up the Drupal 7 core installation for you when updating, but you might want to back-up the sites directory just in case something goes wrong. You also want to take a backup of the database. Use the command below to back up everything:

```text
drush archive-dump
```

#### 2. Put your site in maintenance mode <a id="s-2-put-your-site-in-maintenance-mode"></a>

```text
drush vset --exact maintenance_mode 1 
drush cache-clear all 
```

#### 3. Update Drupal with drush <a id="s-3-update-drupal-with-drush"></a>

```text
drush pm-update drupal
```

Drush will also update your database if necessary.

#### 4. Check that everything works <a id="s-4-check-that-everything-works"></a>

Go around your site and test everything! If you had modified robots.txt or .htaccess, make sure the modifications are reapplied. \(Sometimes you can just copy the old files back.\) If you used a custom installation profile, you might have to copy that back too. If the configuration file has changed, make sure your file has the latest and correct information - compare `sites/default/settings.php` and `sites/default/default.settings.php`.

#### 5. Put your site online again <a id="s-5-put-your-site-online-again"></a>

```text
drush vset --exact maintenance_mode 0 
drush cache-clear all 
```

### Alternative Drush commands <a id="s-alternative-drush-commands"></a>

Alternatively, you might be interested in those other Drush commands:

* `drush pm-update` is the same as running `drush pm-updatecode` and then `drush updatedb`, so you can optionally run the latter two commands to break up the process.
* `drush pm-updatecode` has a number of options you can use with `drush pm-update`, including `--security-only`. Learn more [here](http://drushcommands.com/drush-7x/pm/pm-updatecode/). You can run update commands with `-n` to prevent it from automatically answering 'y' to every 'y/n' request for user input.

### Troubleshooting <a id="s-troubleshooting"></a>

* _No code updates available_ for __"drush pm-update drupal"  
  Run following code which will refresh the available releases_._  
 

  ```text
  drush rf
  ```

  and rerun

  ```text
  drush pm-update drupal

  ```

