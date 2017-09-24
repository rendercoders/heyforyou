---
title: 简单用PHP理解队列的ENQUEUE和DEQUEUE
date: 2017-09-24 14:32:52
tags: [数据结构, 队列]
---
### 什么是队列

`队列`(queue)是一种`动态集合`，实现的是一种`先进先出`(first-in, first-out, FIFO)的策略。

### 队列的ENQUEUE和DEQUEUE

队列上的`INSERT`操作被称为`入队`(ENQUEUE)，`DELETE`操作称为`出队`(DEQUEUE)。`队列`有`队头`(head)和`队尾`(tail)，当有一个元素入队时，它就会被放在队尾的位置。

<!-- more -->
### 举个栗子
我们生活中常见到的买单，先排队的先付钱。

### PHP代码实现
```
// 定义一个简单的队列类
class Queue
{
	protected $overflow;

	protected $data;

	// 设置上溢
	public function set_overflow($overflow)
	{
		$this->overflow = $overflow;
	}

	// 获取上溢
	protected function get_overflow()
	{
		return $this->overflow;
	}

	// 设置数据
	public function set_data($data)
	{
		$this->data = $data;
	}

	// 获取数据
	public function get_data()
	{
		return $this->data;
	}

	// 入队
	public function enqueue($value)
	{
		$array = $this->data;
		// 判断是否为数组
		if (!is_array($array)) {
			$this->data = 'Error, it\'s not an array';
			return;
		}
		// 判断是否上溢
		if ($this->check_is_overflow()) {
			$this->data = 'Error, overflow';
			return;
		}
		$array = array_values($array);
		// 队尾
		$tail = $value;
		if ($tail == count($array)) {
			$tail = 0;
		} else {
			$tail = $tail + 1;
		}
		$array[] = $value;
		$this->data = $array;
	}

	// 出队
	public function dequeue()
	{
		$array = $this->data;
		// 判断是否为数组
		if (!is_array($array)) {
			$this->data = 'Error, it\'s not an array';
			return;
		}
		// 判断是否下溢
		if ($this->check_is_underflow()) {
			$this->data = 'Error, underflow';
			return;
		}
		// 判断是否上溢
		if ($this->check_is_overflow()) {
			$this->data = 'Error, overflow';
			return;
		}
		$array = array_values($array);
		$head = 0;
		$array_count = count($array);
		if ($head == $array_count) {
			$this->data = $array;
		}
		unset($array[$head]);
		$array = array_values($array);
		$this->data = $array;
	}

	// 判断是否下溢
	protected function check_is_underflow()
	{
		$array_count = count($this->data);
		if ($array_count < 0) {
			return true;
		}
		return false;
	}

	// 判断是否上溢
	protected function check_is_overflow()
	{
		$array_count = count($this->data);
		$overflow = $this->overflow;
		if ($overflow && $array_count >= $overflow) {
			return true;
		}
		return false;
	}
}

$queue = new Queue();
// 设置上溢
$queue->set_overflow(10);
// 测试数据
$testArr = ['123123', 'test', 'hello'];
// 设置数据
$queue->set_data($testArr);
// 获取数据
$result = $queue->get_data();
var_dump('测试数据', $result);

// 入队一个
$queue->enqueue(5);
$result = $queue->get_data();
var_dump('入队一个', $result);

// 再入队一个
$queue->enqueue(77);
$result = $queue->get_data();
var_dump('再入队一个', $result);

// 再入队一个
$queue->enqueue('你好');
$result = $queue->get_data();
var_dump('再入队一个', $result);

// 出队一个
$queue->dequeue();
$result = $queue->get_data();
var_dump('出队一个', $result);

// 再出队一个
$queue->dequeue();
$result = $queue->get_data();
var_dump('再出队一个', $result);
```

### 打印的结果
![打印的结果](http://owq1mzbaq.bkt.clouddn.com/%E9%98%9F%E5%88%97-queue.png)