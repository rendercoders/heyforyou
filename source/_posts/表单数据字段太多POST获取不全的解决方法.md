---
title: 表单数据字段太多 POST 获取不全的解决方法
date: 2018-05-02 12:43:53
tags: [PHP]
---
> 表单字段太多，后台 post 获取数据字段不全，是由于 PHP 的 max_input_vars 默认值为 1000，当我们的字段超过1000的时候，我们需要改为更大的数值。

修改 php.ini 文件的
```
# How many GET/POST/COOKIE input variables may be accepted
# 可以接受多少个 GET/POST/COOKIE 的输入变量
max_input_vars = 3000
```