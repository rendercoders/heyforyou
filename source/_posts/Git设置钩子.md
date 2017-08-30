---
title: Git设置钩子
date: 2017-08-30 23:20:35
tags:
---
* 进入到项目目录部署git项目
```
$ cd /var/www/html
$ git clone xxxx
```
* 然后进入到hooks目录中

<!-- more -->
```
$ cd xxxx/.git/hooks
```
* 新建post-receive文件
```
$ vim post-receive
```
* 输入以下内容, :wq保存退出
```
#!/bin/sh
DEPLOY_PATH=/var/www/html/xxx

unset  GIT_DIR
cd $DEPLOY_PATH
git reset --hard
git pull
chown www:www -R $DEPLOY_PATH
```