---
title: "Processing Text"
date: 2021-11-17T00:00:00-06:00
draft: false
weight: 21
---

## Python text processing

Python文本处理可用于：

1. Searching strings for specific information
2. Validating patterns of characters, digits, etc.
3. Transforming content between different formats
4. Manipulating and extracting string content
5. Preparing text for display to the user

## Basic string operations

导入字符串模块：

```
import string
```

字符串模块包含了一些常用的字符串操作，比如下面是一些predefined字符串常量：

```
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

```
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

```
result = s.isalnum()
result = s.isalpha()
result = s.isnumeric()
```

输出结果是bool值，例如，第一个result如果为True，则表示字符串中只包含字母和数字，如果为False，则表示字符串中包含字母和数字以外的字符。

也可以使用`all`函数来检查字符串中是否只包含字母和数字：

```
result = all([c.isalnum() for c in s])
```

## Searching strings

`startswith`和`endswith`函数可以用来检查字符串是否以指定的字符串开头或结尾，如果是，则返回True，否则返回False。例如：

```
s = "The quick brown fox jumps over the lazy dog"
result = s.startswith("The")
print(result)
result = s.endswith("on")
print(result)
```

两次输出结果是：True和False。

`find`和`rfind`函数可以用来检查字符串是否包含指定的字符串，如果是，则返回第一个匹配的字符串的索引，否则返回-1。`find`函数从左向右查找，`rfind`函数从右向左查找。例如：

```
s = "The quick brown fox jumps over the lazy dog"
result = s.find("the")
print(result)
result = s.rfind("the")
print(result)
```

输出结果是：31和31.

检查字符串中是否包含指定的字符串：

```
result = "the" in s
print(result)
```

输出结果是：True.

`replace`函数可以用来替换字符串中的指定字符串，例如：

```
s = "The quick brown fox jumps over the lazy dog"
result = s.replace("the", "a")
print(result)
```

输出结果是：`The quick brown fox jumps over a lazy dog`。

`count`函数可以用来统计字符串中指定的字符串出现的次数，例如：

```
s = "The quick brown fox jumps over the lazy dog"
result = s.count("the")
print(result)
```

输出结果是：1. 
