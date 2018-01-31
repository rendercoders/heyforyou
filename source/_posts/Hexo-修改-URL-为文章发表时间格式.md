---
title: Hexo 修改 URL 为文章发表时间格式
date: 2018-01-25 12:30:49
tags:
---
在 _config.yml 配置 time_format: HH:mm:ss 下面添加

```
post_time_format: YYYYMMDDHHmmss
```

通过在 post_permalink.js 的 postPermalinkFilter 方法下面添加 post_time 变量

```
post_time: data.date.format('YYYYMMDDHHmmss'),
```

然后编译即可。（^_^）