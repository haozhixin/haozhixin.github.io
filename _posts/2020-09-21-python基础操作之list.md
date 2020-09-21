---
title: Python基础操作之list/tuple
author: Cotes Chung
date: 2020-09-21 14:30:00 +0800
categories: [Blogging, Tutorial]
tags: [python基础]
pin: true
---

[TOC]

## 列表  list

列表 作为python常见数据类型之一，可增、删、改

### 基础操作
创建list
```python
empty = []
lst = [1,'xiaoxiao', 23.2, '1234324']
lis2 = ['1','2020-09-1',['列表','元组']]
```
求list内元素个数,使用len()函数
```python
len(empty)   # 0 
len(lst) 	 # 4
len(lst2)	 # 3
```
遍历lst内元素对应的类型，使用for循环进行遍历
```python
>>> lst = [1,'xiaoxiao', 23.2, '1234324']
>>> for _ in lst:
...     print(f'{_}的类型为{type(_)}')
...
1的类型为<class 'int'>
xiaoxiao的类型为<class 'str'>
23.2的类型为<class 'float'>
1234324的类型为<class 'str'>
```
list.append()方法向lis2中的第三个元素['列表','元组'] 后添加['字典']
```python
>>> lis2 = ['1','2020-09-1',['列表','元组']]
>>> print(lis2[2])
['列表', '元组']
>>> suk = lis2[2]
>>> suk.append('字典')
>>> suk
['列表', '元组', '字典']
>>> lis2
['1', '2020-09-1', ['列表', '元组', '字典']]
```
list.insert() 在第一个站位符插入字符串
```python
>>> suk = lis2[2]
>>> suk.insert(1,'insert')
>>> lis2
['1', '2020-09-1', ['列表', 'insert', '元组', '字典']]
```
list.pop() 移除尾部元素
```python
>>> lis2.pop()
['列表', 'insert', '元组', '字典']
>>> lis2
['1', '2020-09-1']
```
list.remove() 移除指定位置字符串或指定字符串
```python
>>> suk
['列表', '元组', '字典', 'xx', 'bb']
>>> suk.remove(suk[4])   #移除4位置上的bb
>>> suk
['列表', '元组', '字典', 'xx']
>>> suk.remove('xx')     #移除'xx'
>>> suk
['列表', '元组', '字典']
```

### 深浅拷贝
#### 浅拷贝
当我们对suk列表进行操作时，发现lis2的值也发生了变化，原因是sku引用的是lis2的第三个元素，suk指向的内存空间发生变化，lis2也会发生变化；
如果不想改变lis2的第三个变量需要复制出lis2这个元素，使用list.copy()即可实现，原因是它们位于不同的内存空间，此实现方式就是shallow copy （浅拷贝）
copy父对象，不会拷贝父对象中的子对象，只copy一层
```python
>>> lis2 = ['1', '2020-09-1', ['列表', '元组', '字典']]
>>> sku_deep = lis2[2].copy()     # 将第三个元素拷贝一份
>>> sku_deep 
['列表', '元组', '字典']
>>> sku_deep[0] = 'abc'   # 改变suk_deep中第0个元素的值
>>> print(sku_deep)
['abc', '元组', '字典']
>>> print(lis2)      # 查看原始lis2列表，数据并未改变
['1', '2020-09-1', ['列表', '元组', '字典']]
```
#### 深拷贝
与shallow copy区别是完全拷贝父对象及其子对象，内存中的状态是完全将对象都复制了一份，在python中需要使用copy模块deepcopy函数：
```python
>>> from copy import deepcopy
>>> a = ['1', '2020-09-1', ['列表', '元组', '字典']]
>>> ab = deepcopy(a)
>>> ab[0] = 10
>>> ab[2][0] = 'mm'
>>> a
['1', '2020-09-1', ['列表', '元组', '字典']]
>>> ab
[10, '2020-09-1', ['mm', '元组', '字典']]
```
### 切片
使用切片来增加python对使用列表的便捷性，操作展示如下：
```python
>>> cc = [1,3,5,7,9,11,13,15]
>>> cc[:3]    #获取列表的前三个元素
[1, 3, 5]
>>> cc[-1]   #获取列表的最后一个元素
15
>>> cc[:-1]   #获取除最后一个以外的其他数据
[1, 3, 5, 7, 9, 11, 13]
>>> cc[1:5]  #获取1-5为索引的数据，不包括索引5的数据
[3, 5, 7, 9]
>>> cc[1:5:2]   #获取索引1-5，步长为2的切片
[3, 7]
>>> cc[::3]    #生成索引[0,len(cc)]步长为3的切片
[1, 7, 13]
>>> cc[::-3]   #生成逆向索引，步长为3的切片
[15, 9, 3]  
>>> cc[::-1]   #可实现列表中数字翻转
[15, 13, 11, 9, 7, 5, 3, 1]
```
>**逆向：**将列表翻转

``` python
def reverse(lit):
    return lit[::-1]

a = [1, 4, 7, 10, 13, 16, 19]
re = reverse(a)
print(re)
----------output-------------
[19, 16, 13, 10, 7, 4, 1]
```


## 元组
元组的属性来看是不可变对象，没有增加、删除元素的方法，但支持切片操作。
统计一个元组内单个元素出现的个数,如没有numpy方法的需要使用：
pip3 install numpy 进行安装
```python
from numpy import random
a = random.randint(1,5,10)   #从1,5区间内随机选择10ge
at = tuple(a)
print(at.count(3))

-----output-----
2
```

