---
title: mysql联结表(一)
date: 2017-09-22 21:56:34
tags:
---
创建联结
联结的创建非常简单，规定要联结的所有表以及它们如何关联即可。
如：
```
SELECT vend_name, prod_name, prod_price
FORM vendors, products
WHERE vendors.vend_id = products.vend_id
ORDER BY vend_name, prod_name;
```
得到:

| vend_name  | prod_name   | prod_price |
| :-------:  | :-------:   | :--------: |
| ACME       | Bird seed   |   10.00    |
| ACME       | Carrots     |   2.50     |
| Anvils     | 1 ton anvil |   14.99    |

<!-- more -->

```
分析：
SELECT 语句与平时的语句一样指定要检索的列。这里最大的差别是所有指定的两个列(prod_name和prod_price) 在一个表中，而另一个列(vend_name) 则在另一个表中。
现在来看FROM子句。与平时的SELECT语句不一样，这条语句的FROM从句列出了两个表，分别是vendors和products。
它们就是这条SELECT语句联结的两个表的名字。
最后，这两个表用WHERE子句正确联结，WHERE子句指示MYSQL匹配venders表中的vend_id和products表中的vend_id。
注意：不要忘记WHERE子句
应该保证所有联结都有WHERE子句，否则MYSQL将返回比想要的数据多得多的数据。同理，应该保证WHERE子句的正确性。不正确的过滤条件将导致MYSQL返回不正确的数据。
```
摘自文献[Mysql必知必会](https://baike.baidu.com/item/MySQL%E5%BF%85%E7%9F%A5%E5%BF%85%E4%BC%9A/6819509?fr=aladdin)