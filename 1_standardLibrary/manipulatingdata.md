---
title: "Manipulating Data"
date: 2021-11-17T00:00:00-06:00
draft: false
weight: 22
---

本节讨论了Python标准库对数据的操作。

## sorted()函数

`sorted()`函数可以对一个列表进行排序。例如：

```python
>>> sorted([3, 1, 2])
[1, 2, 3]
```

`sorted()`函数还可以接受一个key函数作为参数，这样可以按照指定的规则对列表进行排序。例如：

```python
>>> sorted([3, 1, 2], key=lambda x: -x)
[3, 2, 1]
```

`sorted()`函数还可以接受一个reverse参数，如果reverse为True，则表示倒序排序。例如：

```python
>>> sorted([3, 1, 2], reverse=True)
[3, 2, 1]
```

`key`参数还能对一个对象根据指定的属性进行排序。例如：

```python
>>> class Person:
...     def __init__(self, name, age):
...         self.name = name
...         self.age = age
...     def __repr__(self):
...         return 'Person(name={}, age={})'.format(self.name, self.age)
...     def wage(self):
...         return self.age * 10
>>> persons = [Person('Bob', 20), Person('Alice', 30), Person('Carol', 40)]
>>> sorted(persons, key=lambda p: p.name)
[Person(name='Alice', age=30), Person(name='Bob', age=20), Person(name='Carol', age=40)]
>>> sorted(persons, key=lambda p: p.age)
[Person(name='Bob', age=20), Person(name='Alice', age=30), Person(name='Carol', age=40)]
```

`sorted()`函数排序是稳定的，也就是说排序不改变原始数据的相对位置。

> The built-in sorted() function is guaranteed to be stable. A sort is stable if it guarantees not to change the relative order of elements that compare equal - this is helpful for sorting in multiple passes.

## 使用operator模块的函数

导入相关module：

```python
>>> from operator import itemgetter, attrgetter, methodcaller
```

例如使用`attrgetter()`函数，可以根据指定的属性进行排序。例如：

```python
>>> persons = [Person('Bob', 20), Person('Alice', 30), Person('Carol', 40)]
>>> sorted(persons, key=attrgetter('name'))
[Person(name='Alice', age=30), Person(name='Bob', age=20), Person(name='Carol', age=40)]
>>> sorted(persons, key=attrgetter('age'))
[Person(name='Bob', age=20), Person(name='Alice', age=30), Person(name='Carol', age=40)]
```

使用`methodcaller()`函数，可以根据指定的方法进行排序。例如：

```python
>>> persons = [Person('Bob', 20), Person('Alice', 30), Person('Carol', 40)]
>>> sorted(persons, key=methodcaller('wage'))
[Person(name='Bob', age=20), Person(name='Alice', age=30), Person(name='Carol', age=40)]
```

使用`itemgetter()`函数，可以根据指定的元素进行排序。例如：

```python
>>> inventory = [('apple', 3), ('banana', 2), ('pear', 5), ('orange', 1)]
>>> sorted(inventory, key=itemgetter(1))
[('orange', 1), ('banana', 2), ('apple', 3), ('pear', 5)]
>>> sorted(inventory, key=itemgetter(0))
[('apple', 3), ('banana', 2), ('orange', 1), ('pear', 5)]
```

## 使用efficient arrays

array类型的数据结构可以用来存放相同类型的数据，并且可以更高效地进行操作和更少的内存消耗。

首先导入`array`模块并创建一个array对象：

```python
>>> from array import array
>>> a = array('i', [1, 4, 9, 16, 25, 36, 49, 64, 81, 100])
```

输出array对象的类型和长度：

```python
>>> a.typecode
'i'
>>> a.itemsize
4
```

itemsize为4，表示每个元素占4个字节。

在array对象中添加元素：

```python
>>> a.append(121)
>>> a
array('i', [1, 4, 9, 16, 25, 36, 49, 64, 81, 100, 121])
>>> a.insert(0, 0)
>>> a
array('i', [0, 1, 4, 9, 16, 25, 36, 49, 64, 81, 100, 121])
>>> a.extend([-2, -3, -4, -5, -6])
>>> a
array('i', [0, 1, 4, 9, 16, 25, 36, 49, 64, 81, 100, 121, -2, -3, -4, -5, -6])
```

对array中的元素进行遍历：

```python
>>> for i, element in enumerate(a):
...     print(i, element)
...
0 0
1 1
2 4
3 9
4 16
5 25
6 36
7 49
8 64
9 81
10 100
11 121
12 -2
13 -3
14 -4
15 -5
16 -6
```

如果尝试在array对象中添加一个不同类型的元素，会抛出异常：

```python
>>> a.append(3.14)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: integer argument expected, got float
```

如果尝试在array对象中添加超出长度的元素，会抛出异常：

```python
>>> a = array('B', [1, 2, 3, 4, 5])
>>> a.append(300)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
OverflowError: unsigned byte integer is greater than maximum
```

Array对象可以转换为list：

```python
>>> a.tolist()
[1, 2, 3, 4, 5]
```

## Array bisection

如果一个list已经是排好序的，使用bisect模块可以快速地查找一个元素在list中的位置。使用左/右bisection，可以快速地查找一个元素在list中的位置。

```python
>>> import bisect
>>> a = [1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
>>> bisect.bisect(a, 5)
5
>>> bisect.bisect_left(a, 5)
4
>>> bisect.bisect_right(a, 5)
5
```

`bisec.bisect()`和`bisect.bisect_right()`返回的都是被查找元素右边的index，而`bisect.bisect_left()`返回的是被查找元素左边的index。

使用`bisect.insort()`可以快速地插入一个元素到list中，并保持list排序，例如：

```python
>>> a = [1, 4, 9, 16, 25, 36, 49, 64, 81]
>>> bisect.insort(a, 25)
>>> a
[1, 4, 9, 16, 25, 25, 36, 49, 64, 81]
>>> bisect.insort_left(a, 25)
>>> a
[1, 4, 9, 16, 25, 25, 25, 36, 49, 64, 81]
>>> bisect.insort_right(a, 25)
>>> a
[1, 4, 9, 16, 25, 25, 25, 25, 36, 49, 64, 81]
```

`bisect`可以用来作为一个根据breakpoints来进行array lookup，例如我们想知道一个分数最后对应的成绩，可以首先查找分数的位置，然后根据位置查找成绩：

```python
>>> breakpoints = [60, 70, 80, 90]
>>> grades = 'FDCBA'
>>> grades[bisect.bisect(breakpoints, 66)]
'D'
```



