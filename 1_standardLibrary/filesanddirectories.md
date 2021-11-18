---
title: "Files and Directories"
date: 2021-11-17T00:00:00-06:00
draft: false
weight: 23
---

本节讨论Python标准库对文件和目录的操作。Python对文件和目录的操作不需要导入任何模块。


## 打开文件并写入数据

`open()`函数用于打开一个文件，并返回一个文件对象。`w`表示写入模式，`r`表示读取模式，`a`表示追加模式, `r+`表示读写模式。例如写入模式：

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









