---
title: mysql联结表(二)
date: 2017-09-22 22:22:59
tags: [MySQL]
---
内部联结：
上一章讲到的联结称为等值联结(equijoin)，它基于两个表之间的相等测试。这种联结也称为内部联结。
这种联结可以使用稍微不同的语法来明确指定联结的类型。
下面的SELECT语句返回与上一章说的例子相同的数据:
```
SELECT vend_name, prod_name, prod_price
FORM vendors INNER JOIN products
ON vendors.vend_id = products.vend_id;
```
```
分析：
这语句中的SELECT与上一章的SELECT语句相同，但是FROM子句不同。这里两个表之间的关系是FROM子句的组成部分，以INNER JOIN指定。在使用这种语法时，联结条件用特定的ON子句而不是WHERE子句。传递给ON的实际条件和WHERE的相同。
```
<!-- more -->

```
使用哪种语法好：
[ANSI SQL规范](https://baike.baidu.com/item/ANSI%20SQL/5083565?fr=aladdin)首选INNER JOIN语法，此外，尽管使用WHERE子句定义联结的确比较简单，但是使用明确的联结语法能够确保不会忘记联结条件，有时候这样做也能影响性能。
```
摘自文献[Mysql必知必会](https://baike.baidu.com/item/MySQL%E5%BF%85%E7%9F%A5%E5%BF%85%E4%BC%9A/6819509?fr=aladdin)