---
title: 从输入URL到页面加载完成的过程中都发生了什么事情？
date: 2017-09-20 23:24:09
tags:
---
简单的总结下:
1、解析URL
2、DNS查询(浏览器缓存查询/本地host查询/发送DNS 查询请求/查询本地 DNS 服务器等)
3、拿到IP后，浏览器跟服务器建立TCP连接
4、浏览器向web服务器发送http请求
5、HTTP服务器请求处理
6、服务器返回相应文件，并进行页面渲染
<!-- more -->

博文参考:
[输入一个URL到页面呈现其中发生的过程-------http过程详解](http://www.cnblogs.com/heshan1992/p/6829309.html)
[What really happens when you navigate to a URL](http://igoro.com/archive/what-really-happens-when-you-navigate-to-a-url/)
