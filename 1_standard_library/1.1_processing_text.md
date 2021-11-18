---
title: "Processing Text"
date: 2021-11-17T00:00:00-06:00
draft: false
weight: 21
---

本节讨论了Python中的字符串处理函数。

## Python text processing

Python文本处理可用于：

1. Searching strings for specific information
2. Validating patterns of characters, digits, etc.
3. Transforming content between different formats
4. Manipulating and extracting string content
5. Preparing text for display to the user

## Basic string operations

导入字符串模块：

```python
import string
```

字符串模块包含了一些常用的字符串操作，比如下面是一些predefined字符串常量：

```python
string.ascii_letters
string.ascii_lowercase
string.ascii_uppercase
string.digits
string.hexdigits
string.octdigits
string.punctuation
string.printable
string.whitespace
```

在Visual Studio Code中，可以使用`Ctrl+Shift+P`打开command palette，输入`python`，然后选择`Run Python File in Terminal`，这样就可以在terminal中运行python代码了。

如果打印以上字符串常量，可以看到它们的值为：

```
abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghijklmnopqrstuvwxyz
ABCDEFGHIJKLMNOPQRSTUVWXYZ
0123456789
0123456789abcdefABCDEF
01234567
!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~
0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~

```

提取字符串中的ascii字母：

```python
s = "The quick brown fox jumps over the lazy dog on the 1st of December"
result = "".join(c for c in s if c in string.ascii_letters)
print(result)
```

输入结果是：

```
ThequickbrownfoxjumpsoverthelazydogonthestofDecember
```

这样就把所有的ascii字母都提取出来了，其他的数字和空格被排除在外。

检查字符串中是否只包含字母和数字、是否只包含字母、是否只包含数字，分别为：

```python
result = s.isalnum()
result = s.isalpha()
result = s.isnumeric()
```

输出结果是bool值，例如，第一个result如果为True，则表示字符串中只包含字母和数字，如果为False，则表示字符串中包含字母和数字以外的字符。

也可以使用`all`函数来检查字符串中是否只包含字母和数字：

```python
result = all([c.isalnum() for c in s])
```

## Searching strings

`startswith`和`endswith`函数可以用来检查字符串是否以指定的字符串开头或结尾，如果是，则返回True，否则返回False。例如：

```python
s = "The quick brown fox jumps over the lazy dog"
result = s.startswith("The")
print(result)
result = s.endswith("on")
print(result)
```

两次输出结果是：True和False。

`find`和`rfind`函数可以用来检查字符串是否包含指定的字符串，如果是，则返回第一个匹配的字符串的索引，否则返回-1。`find`函数从左向右查找，`rfind`函数从右向左查找。例如：

```python
s = "The quick brown fox jumps over the lazy dog"
result = s.find("the")
print(result)
result = s.rfind("the")
print(result)
```

输出结果是：31和31.

检查字符串中是否包含指定的字符串：

```python
s = "The quick brown fox jumps over the lazy dog"
result = "the" in s
print(result)
```

输出结果是：True.

`replace`函数可以用来替换字符串中的指定字符串，例如：

```python
s = "The quick brown fox jumps over the lazy dog"
result = s.replace("the", "a")
print(result)
```

输出结果是：`The quick brown fox jumps over a lazy dog`。

`count`函数可以用来统计字符串中指定的字符串出现的次数，例如：

```python
s = "The quick brown fox jumps over the lazy dog"
result = s.count("the")
print(result)
```

输出结果是：1. 

## String manipulation

`upper`和`lower`函数可以用来把字符串中的大写字母转换成小写字母，例如：

```python
s = "The quick brown fox jumps over the lazy dog"
result = s.upper()
print(result)
result = s.lower()
print(result)
```

输出结果是：`THE QUICK BROWN FOX JUMPS OVER THE LAZY DOG`和`the quick brown fox jumps over the lazy dog`。

`split`和`join`可以把字符串进行分割和合并，`split`的默认分隔符是空格，`join`前面的字符串是用来指定分割符的，例如：

```python
s = "The quick brown fox jumps over the lazy dog"
result = s.split()
print(result)
result = " ".join(s.split())
print(result)
```

输出结果是：`['The', 'quick', 'brown', 'fox', 'jumps', 'over', 'the', 'lazy', 'dog']`和`The quick brown fox jumps over the lazy dog`。

`ljust`、`rjust`和`center`函数可以用来指定字符串的左、右或者中间对齐，例如：

```python
names = ["John", "Paul", "George", "Ringo"]
biggest_name = max(len(name) for name in names)
for name in names:
    print(name.ljust(biggest_name+2, "-") + ":")
for name in names:
    print(name.rjust(biggest_name+2, "-") + ":")
for name in names:
    print(name.center(biggest_name+2, "-") + ":")
```

输出结果是：

```
John----:
Paul----:
George--:
Ringo---:
----John:
----Paul:
--George:
---Ringo:
--John--:
--Paul--:
-George-:
-Ringo--:
```

使用translation table来替换字符串中的字符，例如：

```python
s = "The quick brown fox jumps over the lazy dog"
result = s.translate(str.maketrans("aeiou", "12345"))
print(result)
```

输出结果是：`Th2 q53ck br4wn f4x j5mps 4v2r th2 l1zy d4g`。

## String formatting

使用template string来格式化字符串，首先导入string模块的Template类：

```python
from string import Template
```

使用Template类来创建一个template，例如：

```python
t = Template("$x, glorious $x!")
```

然后使用substitute方法来替换模板中的变量，例如：

```python
result = t.substitute(x="world")
print(result)
```

输出结果是：`world, glorious world!`。

也可以创建一个dictionary来替换模板中的变量，例如：

```python
args = {"x": "world"}
result = t.substitute(args)
print(result)
```

输出结果是：`world, glorious world!`，和上面的输出结果一样。

使用`format`方法也可以用来格式化字符串，例如：

```python
foo = "foo"
bar = 123
result = "The {} number is {}".format(foo, bar)
print(result)
result = "The {1} number is {0}".format(foo, bar)
print(result)
result = "The {var1} number is {var2}".format(var1=foo, var2=bar)
print(result)
result = "The {var2:x} number is {var2:X}".format(**{"var1": foo, "var2": bar})
print(result)
```

输出结果是：`The foo number is 123`, `The 123 number is foo`，`The foo number is 123`和`The 7b number is 7B`。最后一个是把字符串中的数字转换成十六进制的形式。

## String interpolation

该特性至少需要Ptyhon 3.6版本。导入`datetime`模块（后面需要格式化时间变量）：

```python
import datetime
```

使用f-string来格式化字符串，例如：

```python
now = datetime.datetime.now()
product = "coffee"
price = 4.99
tax = 0.07
result = f"Today's date is {now.strftime('%Y-%m-%d')} and the product is {product} and the price is {price} with tax {price * tax:.2f}"
print(result)
```

输出结果是：`Today's date is 2021-11-17 and the product is coffee and the price is 4.99 with tax 0.35`。

更多字符串有关的操作可以参考[Python文档](https://docs.python.org/3/library/string.html)。
