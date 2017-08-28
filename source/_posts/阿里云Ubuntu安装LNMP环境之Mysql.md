---
title: 阿里云Ubuntu安装LNMP环境之Mysql
date: 2017-08-27 00:01:40
tags:
---
在QQ群很多朋友问阿里云服务器怎么安装LNMP环境，怎么把项目放到服务器上面去，在这里，我就从头开始教大家怎么在阿里云服务器安装LNMP环境。
在这之前，我们先要知道什么是LNMP。
L: 表示的是Linux系统, 包括Ubuntu、Centos但不限于以上两种的系统版本。
N: 表示的是Nginx,这是一个高性能的HTTP和反向代理服务器，也是一个IMAP/POP3/SMTP代理服务器。
M: 表示的是Mysql,Mysql是一个小型关系型数据库管理系统。
P: 表示的是PHP,PHP是一种在服务器端执行的嵌入HTML文档的脚本语言。
<!-- more -->

安装完Nginx之后,我们安装Mysql5.7版本的
```
$ apt install -y mysql-server-5.7
```
接着会弹出两次框, 这是给你设置mysql的root密码的, 输入密码回车即可.
安装完成后, 我们输入:
```
$ mysql -uroot -p
```
再输入密码就可以进入到mysql里面。 退出使用
```
mysql> exit;
```

这个时候我们使用Sequel Pro去连接服务器的mysql是连不上的, 会报:
```
Connection failed!
Unable to connect to host xxx.xxx.xx.xx, or the request timed out.

Be sure that the address is correct and that you have the necessary privileges, or try increasing the connection timeout (currently 10 seconds).

MySQL said: Can't connect to MySQL server on 'xxx.xxx.xx.xx' (61)
```
这是为了安全然后禁止root用户从外网访问, 为了安全, 我们添加一个新的账号从外网登录到服务器的mysql, 先进入mysql命令模式。
```
$ mysql -uroot -p
mysql> GRANT ALL PRIVILEGES ON *.* TO 'test'@'%' IDENTIFIED BY 'test' WITH GRANT OPTION;
mysql> FLUSH PRIVILEGES;
```
上面的命令可[参考](http://blog.csdn.net/wengyupeng/article/details/3290415)

这个时候你会发现使用IP去连接mysql还是不能连接上, 这是因为mysql5.7绑定了ip地址为127.0.0.1, 需要改为0.0.0.0, 才能访问。
这个时候我们就去修改一下:
```
$ vim /etc/mysql/mysql.conf.d/mysqld.cnf
bind-address = 127.0.0.1  改为  bind-address = 0.0.0.0
$ /etc/init.d/mysql restart  //重启mysql
```
这个时候我们再使用工具连接mysql的时候, 就能正常的访问了。

PHP-HTML5学习交流群:
QQ一群群号: 476614753
QQ二群群号: 577094233