## Discovery/Footprinting

A quick way to identify a WordPress site is by browsing to the `/robots.txt` file. A typical robots.txt on a WordPress installation may look like:

```shell-session
User-agent: *
Disallow: /wp-admin/
Allow: /wp-admin/admin-ajax.php
Disallow: /wp-content/uploads/wpforms/

Sitemap: https://inlanefreight.local/wp-sitemap.xml
```

Here the presence of the `/wp-admin` and `/wp-content` directories would be a dead giveaway that we are dealing with WordPress. Typically attempting to browse to the `wp-admin` directory will redirect us to the `wp-login.php` page. This is the login portal to the WordPress instance's back-end.![[wp-login2.webp]]
There are five types of users on a standard WordPress installation.

1. Administrator: This user has access to administrative features within the website. This includes adding and deleting users and posts, as well as editing source code.
2. Editor: An editor can publish and manage posts, including the posts of other users.
3. Author: They can publish and manage their own posts.
4. Contributor: These users can write and manage their own posts but cannot publish them.
5. Subscriber: These are standard users who can browse posts and edit their profiles.

## WPScan

[WPScan](https://github.com/wpscanteam/wpscan) is an automated WordPress scanner and enumeration tool. It determines if the various themes and plugins used by a blog are outdated or vulnerable. It’s installed by default on Parrot OS but can also be installed manually with `gem`.
