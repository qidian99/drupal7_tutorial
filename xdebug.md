# XDebug

## Download XDebug

{% embed url="http://xdebug.org/docs/install" %}

```text
pecl install xdebug
```

Gave me the path: /usr/local/Cellar/php@7.3/7.3.21/pecl/20180731/xdebug.so

```php
zend_extension="/usr/local/Cellar/php@7.3/7.3.21/pecl/20180731/xdebug.so"
```

## Set up in VSCode

{% embed url="https://www.drupal.org/forum/support/module-development-and-code-questions/2019-03-26/please-help-with-configuring-xdebug" %}

{% embed url="https://www.drupal.org/docs/develop/development-tools/configuring-visual-studio-code" %}

## idekey

{% embed url="https://xdebug.org/docs/remote" %}

#### string xdebug.idekey = \*complex\*

Controls which IDE Key Xdebug should pass on to the DBGp debugger handler. The default is based on environment settings. First the environment setting DBGP\_IDEKEY is consulted, then USER and as last USERNAME. The default is set to the first environment variable that is found. If none could be found the setting has as default ''. If this setting is set, it always overrides the environment variables.



I too hit this issue, and xdebug.idekey was the final piece to get this working, here's the full config I've used, but please note I'm debugging a remote Xdebug instance.

```text
xdebug.remote_enable = 1
xdebug.remote_autostart = 1
xdebug.remote_connect_back = 1
xdebug.remote_port = 9000
xdebug.idekey = VSCODE
```

## Tutorial

{% embed url="https://medium.com/@saptashwa04/configure-visual-studio-code-for-drupal-development-8183b5bbe794" %}

{% embed url="https://dev4developer.wordpress.com/2018/02/24/debugging-php-with-visual-studio-code-xdebug/" %}



## XDebug, PHP7, and MacOS

{% embed url="https://stackoverflow.com/questions/46593880/xdebug-on-macos-10-13-with-php-7" %}

Ok so I finally got it running myself it works perfectly! I'm assuming that the xdebug binary that comes with macOS High Sierra \(found under: `/usr/lib/php/extensions/no-debug-non-zts-20160303/xdebug.so`\) is not compatible with PHP7's new Zend engine.

So I downloaded the latest source from the [xdebug website](https://xdebug.org/) and did the following:

1. Installed autoconf with brew;
2. Run `phpize` to configure the build for the new Zend engine;
3. Run `./configure`
4. Run `make`

Now the new binary is under `modules/xdebug.so`

However macOS System Integrity Protection \(SIP\) will prevent you from overwriting the `xdebug.so` under `/usr/lib/php/extensions/`. I didn't want to disable this so I created a new directory path under `/usr/local/lib/php/extensions/` and copied the new binary to this location. I'm not sure if this directory is the best place to put it or if this is bad practice but it worked for me.

Finally I reconfigured my php.ini to use the new binary and everything worked perfectly!



## Acquia

{% embed url="https://www.drupal.org/docs/develop/development-tools/setting-up-netbeans-xdebug-drupal-development-and-templates-for" %}



