### 1.1 Python简介

#### 优点：
* 可移植性：无需任何修改就可以运行在Windows、linux等系统上。
* 易学易上手：语法简单，开源。
* 丰富的工具库：提供各种标准库，包括正则表达式、数据库、线程等等。

#### 缺点：
* 运行速度慢：python是解释型语言，相对于C语言，运行速度比较慢，因为需要在执行时编译成机器码。
* 不能加密：发布解释型语言程序实际上就是发布源代码。


### 1.2 输入和输出

输入：`input`；输出：`print`

``` python
  name = input('please input a char')
  print('hello world!')
```

### 1.3 变量和数据类型

#### 变量与常量

``` python 
  a = 5;
  PI = 3.1415936
```

#### 数据类型

* 整数
* 浮点数
* 字符串
* 布尔值：`True`、`False`
* 空值(none)

### 1.4 list和tuple
> list是python内置的一种数据类型，表示有序集合。

#### list的方法：

* `len()`：获取list元素的个数。
* `append()`：在list末尾添加元素。
* `pop()`：删除list末尾的元素，传入参数可删除指定位置的元素。
* `insert()`：插入元素到指定位置。

``` python
>>>names = ['tom', 'jack', 'mary']
>>>names
['tom', 'jack', 'mary']
```

> tuple也是有序列表，一旦初始化就不可修改。

因为tuple不可变，所以代码更安全。

### 1.5 条件判断

``` python
if age >= 20:
    print('hello')
elif age == 8:
    print('world')
else age <= 7:
    print('!')
```

### 1.6 循环
``` python
for i in list(range(5))
    print(i)
```

`range`：可以生成一个整数序列。

### 1.7 dict和set

> dict实际上就是map，使用键值对存储，查找速度快。

``` python
>>> d = { 'tom': 20, 'jack': 21, 'mary': 22 }

>>> d['tom']
20

>>> 'tom' in d
True

>>> d['carol'] = 20

>>>d.get('tom')
20

>>>d.get('tom', 1)
1
```

#### dict方法
* 如果key值不存在就会报错，可以通过`in`判断key是否存在。  
* `get(key)`方法：如果key不存在，就返回`None`，或者自己指定的value。  
* `pop(key)`方法：删除对应的value。

> set是一组key的集合，不存储value，且key值不能重复。

``` python
>>> s = set([1,1,2,2,3,3])
>>> s
{1, 2, 3}
```

#### set方法
* `add(key)`方法：添加元素，可重复添加，但是不会有效果。  
* `remove(key)`方法：可以删除元素。

``` python
def twoSum(nums, target):
	  if len(nums) <= 1:
	      return False
	  target_dict = {}
	  for i in range(len(nums)):
	      if nums[i] in target_dict:
	          return [target_dict[nums[i]], i]
	      else:
	          target_dict[target - nums[i]] = i

final = twoSum([2, 11, 15, 7], 9)
print(final)
```

#### 1.8 三元表达式

``` python
a = 1
b = 2
value = a if a > b else b
```

等价于其他语言中的

``` javascript
value = a > b ? a: b
```

# 二、函数

### 2.1 函数调用
> 函数调用时参数数量和参数类型必须正确。

### 2.2 内置函数

``` python
>>>int("123")
123

>>>int(12.34)
12

>>>float('12.34')
12.34

>>>str(12.3)
'12.3'

>>>str(100)
'100'

>>>bool(1)
True
```

#### 2.3 函数定义
``` python
def test(value):
   if value > 1:
       return True
   else: 
   	return False
```

> 可以用pass语句定义一个什么都不做的函数

```python
def nop():
    pass
```

* 如果函数没有返回语句，就会返回None。
* 函数可以返回一个值，但实际上是一个tuple。