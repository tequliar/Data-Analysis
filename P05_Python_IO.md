# P5_Python文件读写

#### 这里是Python数据分析学习的第五篇笔记
本文包括了屏幕打印、键盘输出、文件的打开、关闭、读取、写入、重命名删除，以及目录的相关操作。

---
## 打印到屏幕
产生输出的最简单方法是使用`print`语句，可以传递零个或多个由逗号分隔的表达式。此函数将传递的表达式转化为字符串，并将结果写入标准输出，如下所示：
```
#!/usr/bin/python3

print ("Python是世界上最牛逼的语言,", "难道不是吗?")
```
执行上面的代码后，将在标准屏幕上产生一下结果：
```
Python是世界上最牛逼的语言, 难道不是吗?
```

---
## 从键盘读取输入
*Python* 2 有两个内置的函数用于从标准输入读取数据，默认情况下来自键盘。这两个函数分别是：  
`input()`和`raw_input()`。

在 *Python* 3 中，不建议使用`raw_input()`函数。`input()`函数可以从键盘读取数并作为字符串类型，而不管它是否用引号括起来(""或) 
```
>>> x = input("input something:")
input something:yes,input some string
>>> x
'yes,input some string'
>>> x = input("input something:")
input something:1239900
>>> x
'1239900'
>>>
```

---

## 打开和关闭文件
*Python*提供了默认的操作文件所必需的基本功能和方法，可以使用文件对象执行大部份文件操作。

### 打开文件
在读取或写入文件之前，必须使用Python的内置`open()`函数打开文件。此函数创建了一个文件对象，该对象将用于调用与其相关联的其他支持方法
#### 语法
```
file object = open(file_name [, access_mode] [,buffering])
```
这里是参数详细信息：
- file\_name - `file_name`参数是一个字符串值，指定要访问的文件的名称。
- access\_mode - `access\_mode`确定文件打开的模式，即读取，写入，追加等。可能的值的完整列表如下表所示。 这是一个可选参数，默认文件访问模式为(`r` - 也就是只读)。
- buffering - 如果`buffering`值设置为`0`，则不会发生缓冲。 如果缓冲值`buffering`为`1`，则在访问文件时执行行缓冲。如果将缓冲值`buffering`指定为`大于1`的整数，则使用指定的缓冲区大小执行缓冲操作。如果为负，则缓冲区大小为系统默认值(默认行为)

以下是打开文件使用的模式的列表 -

编号 | 模式 | 描述
---|---|---
1|r | 以只读方式打开文件。文件的指针将会放在文件的开头。这是默认模式
2|rb | 以二进制格式打开一个文件用于只读。文件指针将会放在文件的头部。这是默认模式。
3|r+ | 打开一个文件用于读写。文件指针将会放在文件的开头
4|rb+ | 以二进制格式打开一个文件用于读写。文件指针将会放在文件的头部。
5 | w | 打开一个文件只用于写入。如果该文件已存在则将其覆盖。如果该文件不存在，创建新文件。
6|wb | 以二进制格式打开一个文件只用于写入。如果该文件已存在则将其覆盖。如果该文件不存在，创建新文件。
7|w+ | 打开一个文件用于读写。如果该文件已存在则将其覆盖。如果该文件不存在，创建新文件。
8|wb+ | 以二进制格式打开一个文件用于读写。如果该文件已存在则将其覆盖。如果该文件不存在，创建新文件。
9|a | 打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的末尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件用于写入。
10|ab | 以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的末尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件用于写入。
11|a+ | 打开一个文件用于读写。如果该文件已存在，文件指针将会放在文件的末尾，文件打开时会是追加模式。如果该文件不存在，创建新文件用于读写。
12|ab+ | 以二进制格式打开一个文件用于读写。如果该文件已存在，文件指针将会放在文件的末尾，文件打开时会是追加模式。如果该文件不存在，创建新文件用于读写。

### 打开文件属性
打开一个文件并且有一个文件对象后，可以获得与文件相关的各种信息。  
以下是与文件对象相关的所有属性的列表：
编号|属性|描述
---|---|---
1|`file.closed`|	如果文件关闭则返回true，否则返回false。
2|`file.mode`|	返回打开文件的访问模式。
3|`file.name`|返回文件的名称。

> 注意——*Python* 3.x 不支持 `softspace` 属性    

#### 示例 
```
# Open a file
fo = open("foo.txt", "wb")
print ("Name of the file: ", fo.name)
print ("Closed or not : ", fo.closed)
print ("Opening mode : ", fo.mode)
fo.close()
```
执行上面代码，将产生以下结果：
```
Name of the file:  foo.txt
Closed or not :  False
Opening mode :  wb
```

### 关闭文件
文件对象的`close()`方法刷新任何未写入的信息并关闭文件对象，之后不能再进行写入操作。  
当文件的引用对象重新分配给另一个文件时，Python也会自动关闭一个文件。但使用`close()`方法关闭文件是个好习惯。  

#### 语法
```
fileObject.close()
```
#### 示例
```
# Open a file
fo = open("foo.txt", "wb")
print ("Name of the file: ", fo.name)

# Close opened file
fo.close()
```
实行上面代码，产生一下结果：
```
Name of the file:  foo.txt
```

---
## 读取和写入文件
文件对象提供了一组访问方法，使代码编写更方便
### write()方法
`write()`方法将任何字符串写入打开的文件，重要的是要注意，Python字符串可以是二进制数据，而不仅仅是文本。  

`write()`方法不会在字符串的末尾添加换行符('\\n')

#### 语法
```
fileObject.write(string)
```
这里，传递参数 - `string` 是要写入打开文件的内容。

#### 示例  
```
# Open a file
fo = open("foo.txt", "w")
fo.write( "Python is a great language.\nYeah its great!!\n")

# Close opend file
fo.close()
```
上述示例将创建一个 `foo.txt` 文件，并将给定的内容写入到该文件中，最后关闭文件。在执行上面语句后，如果打开文件(`foo.txt`)，它将显示以下内容：
```
Python is a great language.
Yeah its great!!
```

### read()方法
`read()`方法用于从打开的文件读取一个字符串。重要的是要注意Python字符串除文本数据外也可以是二进制数据。
#### 语法
```
fileObiect.read([count])
```
这里，传递参数 - `count`是从打开的文件中读取的字节数。该方法从文件的开始位置开始读取，如果`count`不制定或丢失，则尽可能地尝试读取文件，直到文件结束。
#### 示例
下面读取一个文件`doo.txt`，这是上面示例中创建的。
```
# Open a file
fo = open("foo.txt", "r+")
str = fo.read(10)
print ("Read String is : ", str)

# Close opened file
fo.close()
```
执行上面代码，产生以下效果：
```
Read String is :  Python is
```

---
## 文档位置
`tell()`方法用于获取文件中的当前位置；换句话说，下一次读取或写入将发生在从文件开始处之后的多个字节数的位置。  
`seek(offset [, from])`方法更改当前文件的位置。`offset`参数表示要移动的字节数。`from`参数指定要移动字节的引用位置。  
如果`from`设置为`0`，则将文件的开头作为参考位置。如果设置为 `1`，则将当前位置设置为参考位置。如果设置为 `2`，则文件的末尾将被作为参考位置。  
#### 示例
下面打开一个文件`foo.txt`，这是上面示例中创建的。
```
# Open a file
fo = open("foo.txt", "r+")
str = fo.read(10)
print ("Read String is : ", str)

# Check current position
position = fo.tell()
print ("Current file position : ", position)

# Reposition pointer at the beginning once again
position = fo.seek(0, 0)
str = fo.read(10)
print ("Again read String is : ", str)

# Close opened file
fo.close()
```
执行上面代码，这产生以下结果:
```
Read String is :  Python is
Current file position :  10
Again read String is :  Python is
```

---
## 重命名和删除文件
Python os模块提供用于执行文件处理操作(如重命名和删除文件)的方法。要使用此模块，需要先将它导入，然后可以调用任何相关的函数。

### rename()方法
`rename()`方法有两个参数，即当前的文件名和新的文件名。
#### 语法
```
os.rename(current_file_name, new_file_name)
```
#### 示例
以下是一个将现有文件`test1.txt`重命名为`test2.txt`的示例：
```
import os

# Rename a file from test1.txt to test2.txt
os.rename( "test1.txt", "test2.txt" )
```

### remove()方法
使用`remove()`方法并通过提供要删除的文件的名称作为参数并删除文件。
#### 语法
```
os.remove(file_name)
```

#### 示例
以下是删除现有文件`test2.txt`的示例：
```
import os

# Delete file test2.txt
os.remove("text2.txt")
```

---
## Python中的目录
所有文件都包含在各种目录中，Python处理目录问题也很容易。`OS``模块有几种方法可以用来创建，删除和更改目录。
### mkdir()方法
使用`OS`模块的`mkdir()`方法在当前目录中创建目录。需要为此方法提供一个参数，指定要创建的目录的名称。
#### 语法
```
os.mkdir("newdir")
```
#### 示例
以下是在当前目录中创建一个目录：`test`的示例：
```
import os

# Create a directory "test"
os.mkdir("test")
```

### chdir()方法
使用`chdir()`方法来更改当前目录。`chdir()`方法接受一个参数，它是要选择作为当前目录的目录的名称。
#### 语法
```
os.chdir("nesdir")
```
#### 示例
以下是进入"`/home/newdir`"目录的示例：
```
import os

# Changing a directory to "/home/newdir"
os.chdir("/home/newdir")
```

### getcwd()方法
`getcwd()`方法用于显示当前工作目录。
#### 语法
```
os.getcwd()
```
#### 示例
```
import os

# This would give location of the current directory
os.getcwd()
```

### rmdir()方法
`rmdir()`方法删除该方法中作为参数传递的目录。删除目录之前，应删除所有内容。

#### 语法
```
os.rmdir('dirname')
```
#### 示例
以下是删除“`/tmp/test`”目录的示例。需要给出目录的完全限定名称，否则将在当前目录中搜索该目录。
```
import os

# This would remove "/tmp/test"  directory.
os.rmdir("/tmp/test")
```

## 文件和目录相关方法
有三个重要的来源，它们提供了广泛的实用方法来处理和操作Windows和Unix操作系统上的文件和目录。它们如下 -

- 文件对象和方法 - 文件对象提供了操作文件的功能。
- OS对象和方法 - 这提供了处理文件和目录的方法。