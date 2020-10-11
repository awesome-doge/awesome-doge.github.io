---
layout: post
title: "apache 除錯+ 參數(記憶體+child)"
date: 2020-10-9
tags: [wordpress]
categories: [wordpress]
image: /image/apache.png
description: "apache log 位置 重啟指令 just for bitnami"
---

apache log 位置 重啟指令 just for bitnami
![](/image/apache.png)

重啟server
```
sudo /opt/bitnami/ctlscript.sh restart php-fpm
sudo /opt/bitnami/ctlscript.sh restart apache
```

log 位置：
```
sudo tail -f /opt/bitnami/php/var/log/php-fpm.log
sudo tail -f /opt/bitnami/apache2/logs/error_log
sudo tail -f /home/user/custom-restarts.log
```

參數設定位置：
```
sudo nano /opt/bitnami/php/etc/php-fpm.conf
sudo nano /opt/bitnami/php/etc/common-ondemand.conf
sudo nano /opt/bitnami/php/etc/common-dynamic.conf
sudo nano /opt/bitnami/php/etc/php.ini
sudo nano /opt/bitnami/apache2/conf/httpd.conf
```

wordpress-pool`/opt/bitnami/php/etc/php-fpm.conf`
```
emergency_restart_threshold 10
emergency_restart_interval 1m
process_control_timeout 10s
```
**針對 pool too busy 的問題**
* https://serverfault.com/questions/807453/warning-pool-www-seems-busy-you-may-need-to-increase-pm-start-servers-or-pm-m

記憶體調整`/opt/bitnami/php/etc/php.ini`
```
memory_limit = 2048M
```

## 參考文獻
* [https://geekflare.com/php-fpm-optimization/](Optimizing PHP-FPM for High Performance)
* [PHP FPM Max Children](https://kejyuntw.gitbooks.io/ubuntu-learning-notes/content/web/php/web-php-max-children.html)
* [解決 WordPress 網站記憶體不足的 PHP 錯誤問題](https://blog.gtwang.org/wordpress/fix-wordpress-memory-exhausted-error-increase-php-memory/)
* [Start Or Stop Services](https://docs.bitnami.com/aws/faq/administration/control-services/)