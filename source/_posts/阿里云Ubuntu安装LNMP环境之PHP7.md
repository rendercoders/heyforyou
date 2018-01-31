---
title: 阿里云Ubuntu安装LNMP环境之PHP7
date: 2017-08-27 01:28:51
tags: [PHP]
---
在QQ群很多朋友问阿里云服务器怎么安装LNMP环境，怎么把项目放到服务器上面去，在这里，我就从头开始教大家怎么在阿里云服务器安装LNMP环境。
在这之前，我们先要知道什么是LNMP。
L: 表示的是Linux系统, 包括Ubuntu、Centos但不限于以上两种的系统版本。
N: 表示的是Nginx,这是一个高性能的HTTP和反向代理服务器，也是一个IMAP/POP3/SMTP代理服务器。
M: 表示的是Mysql,Mysql是一个小型关系型数据库管理系统。
P: 表示的是PHP,PHP是一种在服务器端执行的嵌入HTML文档的脚本语言。
<!-- more -->

安装PHP7前, 首先我们要添加PHP的仓库。
```
$ apt install -y software-properties-common
$ add-apt-repository ppa:ondrej/php
$ sudo apt-get update  //更新包管理
```
更新完之后, 我们需要安装PHP7以及需要用到的一些模块:
```
$ apt install -y php7.0 php7.0-mysql php7.0-fpm php7.0-curl php7.0-xml php7.0-mcrypt php7.0-json php7.0-gd php7.0-mbstring php7.0-zip php-mongodb php-memcached php-redis
```
安装完成之后, 查看一下PHP版本:
```
$ php -v
PHP 7.0.22-2+ubuntu16.04.1+deb.sury.org+4 (cli) (built: Aug  4 2017 13:04:09) ( NTS )
Copyright (c) 1997-2017 The PHP Group
Zend Engine v3.0.0, Copyright (c) 1998-2017 Zend Technologies
    with Zend OPcache v7.0.22-2+ubuntu16.04.1+deb.sury.org+4, Copyright (c) 1999-2017, by Zend Technologies
```
紧接着我们需要改下我们的php.ini里面的cgi.fix_pathinfo[至于为什么, 参考博客](http://www.laruence.com/2010/05/20/1495.html)
```
$ vim /etc/php/7.0/fpm/php.ini
#cgi.fix_pathinfo=1  //把#去掉, 并且把值从1改为0
```
修改php-fpm配置
```
$ vim /etc/php/7.0/fpm/pool.d/www.conf
listen = /run/php/php7.0-fpm.sock // 改为listen = /var/run/php/php7.0-fpm.sock
```
改完php-fpm后, 我们需要改一下nginx的配置。
```
$ vim /etc/nginx/sites-enabled/default
root /var/www/html; //这个是网站的根目录, 根据自己的实际情况来改动
index index.html index.htm index.nginx-debian.html; //这个是索引, 如果是要运行.php文件 则要添加index.php在index后台, 改完为index index.php index.html index.htm index.nginx-debian.html;
```
因为nginx本身会把
```
#location ~ \.php$ {
#       include snippets/fastcgi-php.conf;
#
#       # With php7.0-cgi alone:
#       fastcgi_pass 127.0.0.1:9000;
#       # With php7.0-fpm:
#       fastcgi_pass unix:/run/php/php7.0-fpm.sock;
#}
```
注释掉, 所以我们就不动它, 重新加一个也可以:
```
location ~ \.php$ {
    fastcgi_split_path_info ^(.+\.php)(/.+)$;
    fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
    fastcgi_index index.php;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    include fastcgi_params;
}
```
接着我们启动php-fpm:
```
service php7.0-fpm start
```
因为nginx配置已经改过, 所以我们需要重启nginx:
```
service nginx reload
```
测试是否能正常访问php文件, 我们在默认的根目录下面新建一个index.php文件:
```
$ vim /var/www/html/index.php
```
文件里面输出下php信息就可以了, 如:
```
<?php
phpinfo();

```
按esc调出底线命令, 输入:wq 保存文件并退出, 通过浏览器访问: IP地址/index.php, 如果输出有PHP信息则证明已经安装完毕.


PHP-HTML5学习交流群:
QQ一群群号: 476614753
QQ二群群号: 577094233
