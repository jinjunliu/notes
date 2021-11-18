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