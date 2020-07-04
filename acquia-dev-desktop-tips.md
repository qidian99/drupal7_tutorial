# Acquia Dev Desktop Tips

### [Acquia Dev Desktop access from local network](https://rihards.com/2019/acquia-dev-desktop-local-network/)

{% embed url="https://rihards.com/2019/acquia-dev-desktop-local-network/" %}



1. Install, develop, test, etc. your site as usually through Dev Desktop
2. Figure out your local IP on OS X this can be done in terminal by running `ifconfig | grep inet` or opening _Network_ preferences in _System Preferences_, the IP address will be listed under the Status of the connection that you are currently using.

```text
inet 192.168.0.108 netmask 0xffffff00 broadcast 192.168.0.255
```

1. Next you'll want to edit the hosts file of the device you plan to test from. In my case it's Windows 10, so the file is `c:\Windows\System32\Drivers\etc\hosts` and you'll want to add an entry there like: `192.168.100.10 drupal8.dd` replacing the IP address with the one you found earlier, and drupal8.dd with the actual local site URL that you have configured in Dev Desktop.
2. Dev Desktop configures sites to be only accessible from the local machine, so you'll need to edit the Virtual Hosts config file to change this. On OS X this file can typically be found at `/Applications/DevDesktop/apache/conf/vhosts.conf`, find the entry for your site there and right before `Require local` add `Require 192.168` replacing the IP address with the first two numbers of your local network IP. For example, if the IP address from earlier is something like 10.0.0.101 then use `Require 10.0`
3. Restart Acquia Dev Desktop or Stop and Start Apache and MySQL in Dev Desktop
4. Open [http://drupal8.dd:8083](http://drupal8.dd:8083/) \(replacing the address with the one you've configured above\) in your browser.
5. Test your heart out and have fun!





To enable access from all other hosts \(unsafe\)



```text
<VirtualHost *:8083>
  ServerName drupal-7-72.dd
  SSLEngine off
  DocumentRoot "/Users/qidian/Sites/devdesktop/drupal-7.72"
  <IfModule fcgid_module>
    FcgidInitialEnv PHPRC "/Applications/DevDesktop/php7_2_x64/bin"
    FcgidWrapper "\"/Applications/DevDesktop/php7_2_x64/bin/php-cgi\""
  </IfModule>
  <Directory "/Users/qidian/Sites/devdesktop/drupal-7.72">
    Options Indexes FollowSymLinks ExecCGI
    AllowOverride All
    Require all granted
  </Directory>
</VirtualHost>

```

### 

