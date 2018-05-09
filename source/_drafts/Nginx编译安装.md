---
title: Nginx编译安装
abbrlink: 3a1b20dd
date: 2017-10-27 10:53:37
tags:
---
先占坑 后面有时间在写

<!-- more -->
所有工具都放这里
```
$ cd /usr/local/src
```

下载pcre 主要用重写rewrite
$ wget ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre2-10.22.tar.gz

解压
```
$ tar -zxvf pcre2-10.22.tar.gz
```

进入文件夹
```
$ cd pcre2-10.22
```

```
$ ./configure
```

```
$ make && make install
$ cd ..
```

安装zlib库 主要用gzip压缩
```
$ wget http://zlib.net/zlib-1.2.11.tar.gz
```

解压文件
```
$ tar -zxvf zlib-1.2.11.tar.gz
```

进入文件夹
```
$ cd zlib-1.2.11
```

```
$ ./configure
```

```
$ make && make install
$ cd ..
```

下载
```
$ wget http://nginx.org/download/nginx-1.12.2.tar.gz
```

解压
```
$ tar xvf nginx-1.12.2.tar.gz
```

进入nginx文件夹
```
$ cd nginx-1.12.2
```
