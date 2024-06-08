## Discovery/Footprinting

Let's assume that we come across an e-commerce site during an external penetration test. At first glance, we are not exactly sure what is running, but it does not appear to be fully custom. If we can fingerprint what the site is running on, we may be able to uncover vulnerabilities or misconfigurations. Based on the limited information, we assume that the site is running Joomla, but we must confirm that fact and then figure out the version number and other information such as installed themes and plugins.

We can often fingerprint Joomla by looking at the page source, which tells us that we are dealing with a Joomla site.

mylesnieman@htb[/htb]`$ curl -s http://dev.inlanefreight.local/ | grep Joomla  	<meta name="generator" content="Joomla! - Open Source Content Management" />   <SNIP>`

The `robots.txt` file for a Joomla site will often look like this:

```shell-session
# If the Joomla site is installed within a folder
# eg www.example.com/joomla/ then the robots.txt file
# MUST be moved to the site root
# eg www.example.com/robots.txt
# AND the joomla folder name MUST be prefixed to all of the
# paths.
# eg the Disallow rule for the /administrator/ folder MUST
# be changed to read
# Disallow: /joomla/administrator/
#
# For more information about the robots.txt standard, see:
# https://www.robotstxt.org/orig.html

User-agent: *
Disallow: /administrator/
Disallow: /bin/
Disallow: /cache/
Disallow: /cli/
Disallow: /components/
Disallow: /includes/
Disallow: /installation/
Disallow: /language/
Disallow: /layouts/
Disallow: /libraries/
Disallow: /logs/
Disallow: /modules/
Disallow: /plugins/
Disallow: /tmp/
```

We can also often see the telltale Joomla favicon (but not always). We can fingerprint the Joomla version if the `README.txt` file is present.

mylesnieman@htb[/htb]`$ curl -s http://dev.inlanefreight.local/README.txt | head -n 5  1- What is this? 	* This is a Joomla! installation/upgrade package to version 3.x 	* Joomla! Official site: https://www.joomla.org 	* Joomla! 3.9 version history - https://docs.joomla.org/Special:MyLanguage/Joomla_3.9_version_history 	* Detailed changes in the Changelog: https://github.com/joomla/joomla-cms/commits/staging`

In certain Joomla installs, we may be able to fingerprint the version from JavaScript files in the `media/system/js/` directory or by browsing to `administrator/manifests/files/joomla.xml`.

mylesnieman@htb[/htb]`$ curl -s http://dev.inlanefreight.local/administrator/manifests/files/joomla.xml | xmllint --format -  <?xml version="1.0" encoding="UTF-8"?> <extension version="3.6" type="file" method="upgrade">   <name>files_joomla</name>   <author>Joomla! Project</author>   <authorEmail>admin@joomla.org</authorEmail>   <authorUrl>www.joomla.org</authorUrl>   <copyright>(C) 2005 - 2019 Open Source Matters. All rights reserved</copyright>   <license>GNU General Public License version 2 or later; see LICENSE.txt</license>   <version>3.9.4</version>   <creationDate>March 2019</creationDate>     <SNIP>`

The `cache.xml` file can help to give us the approximate version. It is located at `plugins/system/cache/cache.xml`.

## Enumeration

Let's try out [droopescan](https://github.com/droope/droopescan), a plugin-based scanner that works for SilverStripe, WordPress, and Drupal with limited functionality for Joomla and Moodle.

We can clone the Git repo and install it manually or install via `pip`.

mylesnieman@htb[/htb]`$ sudo pip3 install droopescan  Collecting droopescan   Downloading droopescan-1.45.1-py2.py3-none-any.whl (514 kB)      |████████████████████████████████| 514 kB 5.8 MB/s 	  <SNIP>`

Once the installation is complete, we can confirm that the tool is working by running `droopescan -h`.

mylesnieman@htb[/htb]`$ droopescan -h  usage: droopescan (sub-commands ...) [options ...] {arguments ...}      |  ___| ___  ___  ___  ___  ___  ___  ___  ___  ___ |   )|   )|   )|   )|   )|___)|___ |    |   )|   ) |__/ |    |__/ |__/ |__/ |__   __/ |__  |__/||  /                     | =================================================  commands:    scan     cms scanning functionality.    stats     shows scanner status & capabilities.  optional arguments:   -h, --help  show this help message and exit   --debug     toggle debug output   --quiet     suppress all output  Example invocations:    droopescan scan drupal -u URL_HERE   droopescan scan silverstripe -u URL_HERE  More info:    droopescan scan --help   Please see the README file for information regarding proxies.`

We can access a more detailed help menu by typing `droopescan scan --help`.

Let's run a scan and see what it turns up.

mylesnieman@htb[/htb]`$ droopescan scan joomla --url http://dev.inlanefreight.local/  [+] Possible version(s):                                                             3.8.10     3.8.11     3.8.11-rc     3.8.12     3.8.12-rc     3.8.13     3.8.7     3.8.7-rc     3.8.8     3.8.8-rc     3.8.9     3.8.9-rc  [+] Possible interesting urls found:     Detailed version information. - http://dev.inlanefreight.local/administrator/manifests/files/joomla.xml     Login page. - http://dev.inlanefreight.local/administrator/     License file. - http://dev.inlanefreight.local/LICENSE.txt     Version attribute contains approx version - http://dev.inlanefreight.local/plugins/system/cache/cache.xml  [+] Scan finished (0:00:01.523369 elapsed)`

As we can see, it did not turn up much information aside from the possible version number. We can also try out [JoomlaScan](https://github.com/drego85/JoomlaScan), which is a Python tool inspired by the now-defunct OWASP [joomscan](https://github.com/OWASP/joomscan) tool. `JoomlaScan` is a bit out-of-date and requires Python2.7 to run. We can get it running by first making sure some dependencies are installed.

mylesnieman@htb[/htb]`$ sudo python2.7 -m pip install urllib3 $ sudo python2.7 -m pip install certifi $ sudo python2.7 -m pip install bs4`

While a bit out of date, it can be helpful in our enumeration. Let's run a scan.


```shell-session
Warning
Username and password do not match or you do not have an account yet.
```

The default administrator account on Joomla installs is `admin`, but the password is set at install time, so the only way we can hope to get into the admin back-end is if the account is set with a very weak/common password and we can get in with some guesswork or light brute-forcing. We can use this [script](https://github.com/ajnik/joomla-bruteforce) to attempt to brute force the login.

mylesnieman@htb[/htb]`$ sudo python3 joomla-brute.py -u http://dev.inlanefreight.local -w /usr/share/metasploit-framework/data/wordlists/http_default_pass.txt -usr admin   admin:admin`

And we get a hit with the credentials `admin:admin`. Someone has not been following best practices!