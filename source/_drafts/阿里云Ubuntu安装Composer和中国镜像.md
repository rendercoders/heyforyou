---
title: 阿里云Ubuntu安装Composer和中国镜像
tags:
  - PHP
  - Composer
abbrlink: 9353f795
date: 2017-08-27 09:19:50
---
引用: Composer是PHP用来管理依赖（dependency）关系的工具。你可以在自己的项目中声明所依赖的外部工具库（libraries），Composer 会帮你安装这些依赖的库文件。
PHP使用composer的地方越来越多, 接下来我就教大家如果在阿里云上面安装composer并且改为中国镜像。
<!-- more -->
老规矩, 先连上服务器:
```
$ ssh root@xxx.xxx.xx.xx
```
使用apt-get安装composer:
```
$ apt install -y composer
```
安装完成后, 输入composer回车就能看到当前安装的composer的一些信息:
```
$ composer
```
这个时候我们已经安装完成了, 但是由于composer的服务器是在国外, 所以我们使用composer的时候经常断掉或者需要拉取很久才能把代码拉取下来。
这个时候, 国人的智慧就体现出来了, 中国镜像就这样被开发出来了。 具体大家可以去[中国镜像](https://pkg.phpcomposer.com/) 看看。

在这里因为经常使用composer, 所以我就只把全局配置的用法写出来就可以了。
很简洁的一句代码:
```
$ composer config -g repo.packagist composer https://packagist.phpcomposer.com
```
回车, 马上就能享受飞一般的感觉。

PHP-HTML5学习交流群:
QQ一群群号: 476614753
QQ二群群号: 577094233