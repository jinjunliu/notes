---
title: "Files and Directories"
date: 2021-11-17T00:00:00-06:00
draft: false
weight: 23
---

本节讨论Python标准库对文件和目录的操作。Python对文件和目录的操作不需要导入任何模块。


## 文件基本操作

`open()`函数用于打开一个文件，并返回一个文件对象。`w`表示写入模式，`r`表示读取模式，`a`表示追加模式（append）, `r+`表示读写模式。例如写入模式：

```python
f = open('test.txt', 'w')
f.write('Hello, world!')
f.close()
```

这样，我们就成功地创建了一个名为`test.txt`的文件，并写入了一行`Hello, world!`在文件的开头。

如果只读一个文件，可以使用`r`模式，如下将读出文件的内容，并将其打印出来：

```python
f = open('test.txt', 'r')
print(f.read())
f.close()
```

也可以使用`with`语句，这样可以自动地关闭文件：

```python
with open('test.txt', 'r') as f:
    print(f.read())
```

`a`模式下，如果文件不存在，则会创建一个新文件，如果文件存在，则会在文件末尾追加内容。

```python
with open('test.txt', 'a') as f:
    f.write('add something')
```

这时，`test.txt`文件中的内容为`Hello, world!add something`。

使用`seek()`函数可以将文件指针移动到指定位置，例如：

```python
with open('test.txt', 'r') as f:
    f.seek(5)
    print(f.read())
```

这是将文件指针移动到第5个字符（首个字符是第0个字符），然后读取其后面的内容。输出结果为`, world!add something`。

## 创建临时文件和目录

这部分需要导入`os`和`tempfile`模块。

```python
import os
import tempfile
```

获取临时数据环境的信息：

```python
print(tempfile.gettempdir())
print(tempfile.gettempprefix())
```

这里将输出临时数据环境的路径，例如`/tmp`，以及临时文件的前缀，例如`tmp`。

使用`mkstemp()`函数创建临时文件：

```python
(tempfh, tempfp) = tempfile.mkstemp(".tmp", "testTemp", None, True)
print(tempfp)
```

`mkstemp()`函数返回一个元组，其中第一个元素是文件描述符，第二个元素是文件路径。其参数分别是：文件后缀，文件名前缀，指定目录，文件是否是text文件。

使用`os`的`fdopen()`函数将文件描述符转换为文件对象。我们先将临时文件的内容写入，然后读取，并打印出来，最后关闭临时文件，并删除临时文件。

```python
f = os.fdopen(tempfh, "w+t")
f.write("Hello, world!")
f.seek(0)
print(f.read())
f.close()
os.remove(tempfp)
```

使用`TemporaryFile()`函数也可以创建临时文件：

```python
with tempfile.TemporaryFile() as f:
    f.write("Hello, world!")
    f.seek(0)
    print(f.read())
```

如果有很多临时文件需要创建，可以使用`TemporaryDirectory()`函数，它会创建一个临时目录，并在退出时删除该目录。

```python
with tempfile.TemporaryDirectory() as tmpdirname:
    print("created temporary directory", tmpdirname)
    path = os.path.join(tmpdirname, "test.txt")
    with open(path, "w") as f:
        f.write("Hello, world!")
    print("File contents:")
    with open(path, "r") as f:
        print(f.read())
```

## 读取CSV文件

这里需要使用到`csv`模块。

```python
import csv
```

