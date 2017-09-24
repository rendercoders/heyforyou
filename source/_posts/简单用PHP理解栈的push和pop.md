---
title: 简单用PHP理解栈的PUSH和POP
date: 2017-09-24 13:42:45
tags: [数据结构, 栈]
---
#### 什么是栈

`栈`(stack)是一种`动态集合`，实现的是一种`后进先出`(last-in, first-out, LIFO)的策略。

#### 栈的PUSH和POP

栈上的`INSERT`操作被称为`压入`(PUSH)，而无元素参数的`DELETE`操作称为`弹出`(POP)。

<!-- more -->
#### 举个栗子
我们生活中常见到的发传单，假设我去发传单，我把传单拿在手上。
我发出去的时候是从上往下发，发的差不多了，监工看到我手里的传单不多，
把另外一叠传单放到到我剩下的传单上面(后进)，于是我继续从上往下发(先出)。
在最上面的就是先发出去的。

```
<?php
// 栈压入
function stack_push($array, $value)
{
	$max = get_max_key($array);
	$max = $max + 1;
	$array[$max] = $value;
	return $array;
}

// 栈弹出
function stack_pop($array)
{
	$max = get_max_key($array);
	if(check_is_empty_stack($max)){
		return 'Error, underflow'; // 栈下溢
	}
	unset($array[$max]);
	return $array;
}

// 检测是否为空栈
function check_is_empty_stack($value)
{
	if ($value == 0) {
		return true;
	}
	return false;
}

// 获取最大的key
function get_max_key($arr)
{
	$max_key = 0;
	foreach ($arr as $key => $value) {
		if ($key > $max_key) {
			$max_key = $key;
		}
	}
	return $max_key;
}

$testArr = array(1, 23, '24324' => 2324, '424' => 234234);
var_dump('测试数据', $testArr);

// 压入一个
$result = stack_push($testArr, 8);
var_dump('压入一个', $result);

// 再压入一个
$result = stack_push($result, 'test');
var_dump('再压入一个', $result);

// 弹出一个
$result = stack_pop($result);
var_dump('弹出一个: ', $result);

//再弹出一个
$result = stack_pop($result);
var_dump('再弹出一个: ', $result);

//再弹出一个
$result = stack_pop($result);
var_dump('再弹出一个: ', $result);
```
打印的结果为:
![栈结果打印](http://owq1mzbaq.bkt.clouddn.com/%E6%A0%88-stack.png)