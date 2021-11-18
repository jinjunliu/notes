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
