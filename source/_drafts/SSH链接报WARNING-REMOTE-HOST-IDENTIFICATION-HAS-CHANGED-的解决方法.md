---
title: 'SSH链接报WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!的解决方法'
tags:
  - GIT
abbrlink: e7cb4d5b
date: 2017-09-14 11:15:22
---
今天心血来潮,把阿里云服务器云盘给重置了,导致使用SSH链接不上服务器。
连接时报以下错误:
<!-- more -->

```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ECDSA key sent by the remote host is
SHA256:hHXOEiKT2M6fXLiI60aamTH3vN/hSkiwNZfJFiDikkU.
Please contact your system administrator.
Add correct host key in /Users/lhc/.ssh/known_hosts to get rid of this message.
Offending ECDSA key in /Users/lhc/.ssh/known_hosts:14
ECDSA host key for xxx.xxx.xx.xx has changed and you have requested strict checking.
Host key verification failed.
```
解决办法就是按照提示进入.ssh文件把所要连接的IP地址在known_hosts中注释或者删去.
举个栗子: 我的known_hosts在
```
$ vim ~/.ssh/known_hosts
```
