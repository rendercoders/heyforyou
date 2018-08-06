---
title: 如何在Ubuntu 16.04搭建Shadowsocks
tags:
  - Ubuntu
  - Shadowsocks
abbrlink: d5777532
date: 2017-09-23 14:43:27
---
闲的，今天就教大家如何使用国外服务器搭建一个shadowsocks。
# 第一种配置方法.
## 第一步更新软件源
```
$ sudo apt update
```

## 第二步安装pip
```
$ sudo apt -y install python-pip
```
<!-- more -->
## 第三步
```
$ sudo pip install --upgrade pip
```

## 第四步
```
$ sudo pip install setuptools
```

## 第五步安装shadowsocks
```
$ sudo pip install shadowsocks
```

## 第六步配置shadowsocks，并开启
```
sudo ssserver -p 端口号 -k 密码 -m 加密方法 -d start
```
`端口号` 默认 `8388` 我比较喜欢换成 `8888`
`加密方法` 默认 `rc4-md5` 建议改成 `aes-256-cfb`

# 第二种配置方法: 使用配置文件
## 第一到第五步配置跟上面的一样
配置文件必须是json格式，否则会报错
```
{
	"server":"服务器IP地址",
	"server_port": 端口号,
	"local_address": "127.0.0.1",
	"local_port":1080,
	"password": "密码",
	"timeout":300,
	"method": "aes-256-cfb"
}
```
各字段的含义：
`server`：服务器IP地址
`server_port`：服务器端口号
`local_address`：本地监听的IP地址
`password`：加密的密码
`timeout`：超时时间（秒）
`method`：加密方法，可选择 `bf-cfb`, `aes-256-cfb`, `des-cfb`, `rc4`, 等等。默认是一种不安全的加密，推荐用 `aes-256-cfb`

* 创建一个json文件
```
$ vim /etc/shadowsocks.json
```
* 把上面的配置好的JSON内容复制到shadowsocks.json文件中,保存退出

* 启动shadowsocks
```
$ sudo ssserver -c /etc/shadowsocks.json -d start
```

## 第七步，使用shadowsocks客户端连接服务器
![shadowsocks客户端](http://owq1mzbaq.bkt.clouddn.com/shadowsocks.png)

