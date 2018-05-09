---
title: 阿里云Ubuntu安装LNMP环境之Nginx
tags:
  - PHP
  - Nginx
abbrlink: 120f43f7
date: 2017-08-26 22:23:16
---
在QQ群很多朋友问阿里云服务器怎么安装LNMP环境，怎么把项目放到服务器上面去，在这里，我就从头开始教大家怎么在阿里云服务器安装LNMP环境。
在这之前，我们先要知道什么是LNMP。
L: 表示的是Linux系统, 包括Ubuntu、Centos但不限于以上两种的系统版本。
N: 表示的是Nginx,这是一个高性能的HTTP和反向代理服务器，也是一个IMAP/POP3/SMTP代理服务器。
M: 表示的是Mysql,Mysql是一个小型关系型数据库管理系统。
P: 表示的是PHP,PHP是一种在服务器端执行的嵌入HTML文档的脚本语言。
<!-- more -->

首先, 我们使用ssh连接到服务器:
```
$  ssh root@xxx.xxx.xxx.xxx
```
接着我们需要更新一下apt管理工具包:
```
$ apt update
```
更新完之后,使用包管理工具直接下载Nginx:
```
$ apt install -y nginx
```
这个时候可以看一下外面安装的nginx在放在哪里:
```
$ whereis nginx
nginx: /usr/sbin/nginx /etc/nginx /usr/share/nginx
```
现在我们先不管配置, 打开浏览器, 输入服务器IP地址访问, 如果出现:
Welcome to nginx!
那就证明已经安装成功了Nginx。

先简单说一下配置:
现在我使用的nginx版本是1.10.3
```
$ nginx -v
nginx version: nginx/1.10.3 (Ubuntu)
```
这个版本的配置在/etc/nginx/sites-enabled/default
```
$ cd /etc/nginx/sites-enabled/
$ ls
default
```
这个default里面就有我们一会要配置的东西.

还有就是关于Nginx的错误日志的路径/var/log/nginx, 很多时候我们找错误都是从错误日志中找到问题的解决方法，所以这个路径还是要记住的。
```
$ cd /var/log/nginx
$ ls
access.log  error.log
```

PHP-HTML5学习交流群:
QQ一群群号: 476614753
QQ二群群号: 577094233
