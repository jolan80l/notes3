# 1.安装Python

## 版本选择

选择Python3版本

## windows安装

到官网下载python的安装版本，官网地址：https://www.python.org/

推荐参考文章：https://zhuanlan.zhihu.com/p/569019068

## mac安装

推荐文章：https://zhuanlan.zhihu.com/p/532840161#:~:text=%E5%9C%A8Mac%E4%B8%8A%E8%BF%9B%E8%A1%8CPython%E5%A4%9A%E7%89%88%E6%9C%AC%E5%88%87%E6%8D%A2%201%201%E3%80%81%E5%AE%89%E8%A3%85Homebrew%202,2%E3%80%81%E9%80%9A%E8%BF%87brew%E5%AE%89%E8%A3%85pyenv%203%203%E3%80%81%E4%BD%BF%E7%94%A8pyenv%E5%AE%89%E8%A3%85Python3%204%204%E3%80%81%E8%A7%A3%E5%86%B3Python%E7%94%A8pip%E5%91%BD%E4%BB%A4%E5%AE%89%E8%A3%85%E9%80%9F%E5%BA%A6%E6%85%A2%EF%BC%8C%E6%94%B9%E7%94%A8%E5%9B%BD%E5%86%85%E9%95%9C%E5%83%8F

前提电脑上安装了brew，推荐安装文章：https://blog.csdn.net/muyimo/article/details/125211460

```shell
vi ~/.bash_profile
```
在最后增加(然后保存退出) ：
    export PYENV_ROOT=~/.pyenv
    export PATH=$PYENV_ROOT/shims:$PATH
    eval "$(pyenv init -)"

source .bash_profile

查看可安装的Python版本：pyenv install --list

安装相应的版本(可去上面的官网查看版本)：pyenv install 3.10.12 -v

更新：pyenv rehash

切换python版本:

    pyenv global 3.10.12
    pyenv global system

查看当前python版本： python --version

如果没有生效，可能是已经安装了其他版本的Python，需要删除：

ls /Library/Frameworks/Python.framework/Versions/
sudo rm -rf /Library/Frameworks/Python.framework/Versions/版本号

然后重复执行pyenv global 3.10.12，最后重启shell即可

import os os.environ['TK_SILENCE_DEPRECATION'] = '1'

# 安装IDE

使用一款语言进行开发时，需要选择一个合适的IDE，这里选择使用PyCharm。

下载地址：https://www.jetbrains.com/pycharm/download/?section=mac

试用方法：https://blog.csdn.net/For_if_while/article/details/121513041

# Python基础

笔者在学习Python前具有java语言的相关经验，所以可能着重记录与Java的不同之处，相同之处忽略了。笔记以《Python编程快速上手：让繁琐的工作自动化》为基础。

## 表达式

在Python中，2 + 2称为“表达式”，它是语言中最基本的编程结构。表达式包含“值”（例如2）和“操作符”（例如+）。

![avatar](img/1.png)

## 整形、浮点型、字符串

每个值都只属于一种数据类型。下图是常用的数据类型：int， float， strs（总是用单引号（'）包围住字符串）。

![avatar](img/2.png)

## 字符串连接和复制

加号在用于两个字符串时，它将字符串连接起来，成为“字符串连接”操作符。

'Alice' + 'Bob'
'AliceBob

字符串和数字连接将会报错
'Alice' + 42
Traceback (most recent call last):
   File "<pyshell#26>", line 1, in <module>
     'Alice' + 42
TypeError: Can't convert 'int' object to str implicitly

## 变量

spam = 'Hello'

变量只能是一个词，只能包含字母、数字、下划线，不能以数字开头。变量名区分大小写。

## 第一个程序

```python
# This program says hello and asks for my name.
print('Hello world!')
# ask for their name
print('What is your name?')
myName = input()
print('It is good to meet you, ' + myName)
print('The length of your name is:')
print(len(myName))
# ask for their age
print('What is your age?')
myAge = input()
print('You will be ' + str(int(myAge) + 1) + ' in a year.')

```
![avatar](img/3.png)

注释：使用#表示注释

print()：将括号内的字符串显示在屏幕上

input()：函数等待用户在键盘上输入一些文本，并按下回车键。

len()：字符串中字符的个数。

str(29)：表示把整形转为字符串形式。

int()：把字符串转为整形。如果传入的参数不能被转换为整形，则会报错。

int('99.99')
Traceback (most recent call last):
  File "<pyshell#18>", line 1, in <module>
    int('99.99')
ValueError: invalid literal for int() with base 10: '99.99'

float()：字符串转换为浮点数。

## 文本和数字相等判断

42 == '42'
False
42 == 42.0
True
42.0 == 0042.000
True

# 控制流

## 布尔值

略

## 比较操作符

![avatar](img/4.png)

整型或浮点型的值永远不会与字符串相等。表达式42 == '42'求值为False是因为，Python认为整数42与字符串'42'不同。

另一方面，<、>、<=和>=操作符仅用于整型和浮点型值。int和float可以比较。

## not操作符

```shell
>>> not 　True
　False
>>> not not not not True
　True
```

## and和or操作符

```shell
>>> (4 < 5) and (5 < 6)
True
>>> (4 < 5) and (9 < 6)
False
>>> (1 == 2) or (2 == 2)
True
```

## 控制流的元素

### 条件

略

### 代码块

一些代码行可以作为一组，放在“代码块”中。可以根据代码行的缩进，知道代码块的开始和结束。代码块有3条规则。

1．缩进增加时，代码块开始。

2．代码块可以包含其他代码块。

3．缩进减少为零，或减少为外面包围代码块的缩进，代码块就结束了。

看一些有缩进的代码，更容易理解代码块。所以让我们在一小段游戏程序中，寻找代码块，如下所示：

```python
　if name == 'Mary':
    print('Hello Mary')
　if password == 'swordfish':
    print('Access granted.')
　else:
    print('Wrong password.')
```

## 控制流语句

### if语句

最常见的控制流语句是if语句。if语句的子句（也就是紧跟if语句的语句块），将在语句的条件为True时执行。如果条件为False，子句将跳过。

if关键字；
条件（即求值为True或False的表达式）；
冒号；
在下一行开始，缩进的代码块（称为if子句）。

### else语句

if子句后面有时候也可以跟着else语句。只有if语句的条件为False时，else子句才会执行。

```python
if name == 'Alice':
    print('Hi, Alice.')
else:
    print('Hello, stranger.')
```

### elif语句

相当于java中的else if。

```shell
if name == 'Alice':
    print('Hi, Alice.')
elif age < 12:
    print('You are not Alice, kiddo.')
```

### while循环

利用while语句，可以让一个代码块一遍又一遍的执行。只要while语句的条件为True，while子句中的代码就会执行。在代码中，while语句总是包含下面几部分：

关键字；
条件（求值为True或False的表达式）；
冒号；
从新行开始，缩进的代码块（称为while子句）。

```python
spam=0
while spam < 5:
    print('Hello, world.')
    spam=spam + 1
```

带break的while：

```python
while True:
    print('Please type your name.')
    name = input()
    if name == 'your name':
        break
print('Thank you!')
```

带continue的while

```python
while True:
    print('Who are you?')
    name = input()
    if name != 'Joe':
        continue
    print('Hello, Joe. What is the password? (It is a fish.)')
    password = input()
    if password == 'swordfish':
        break
print('Access granted.')

```

### 默认数据类型的布尔值

其他数据类型中的某些值，条件认为它们等价于True和False。在用于条件时，0、0.0和' '（空字符串）被认为是False，其他值被认为是True。比如下面这段程序的结果是True。

```python
name = ''
print(not name)

```

在代码中，for语句看起来像for i in range(5):这样，总是包含以下部分：

for关键字；
一个变量名；
in关键字；
调用range()方法，最多传入3个参数；
冒号；
从下一行开始，缩退的代码块（称为for子句）。

```python
print('My name is')
for i in range(5):
    print('Jimmy Five Times (' + str(i) + ')')
```

rang()函数最多可以输入三个参数。如果只有一个参数表示循环的上线，如果是两个参数表示循环的范围，如果是三个参数表示上限、下限、以及步长。

```python
for i in range(0, 10, 2):
    print(i)


```

```
0
2
4
6
8
```

## 导入模块

Python程序可以调用一组基本的函数，这称为“内建函数”，包括你见到过的print()、input()和len()函数。Python也包括一组模块，称为“标准库”。每个模块都是一个Python程序，包含一组相关的函数，可以嵌入你的程序之中。例如，math模块有数学运算相关的函数，random模块有随机数相关的函数，等等。

在开始使用一个模块中的函数之前，必须用import语句导入该模块。在代码中，import语句包含以下部分：

import关键字；
模块的名称；
可选的更多模块名称，之间用逗号隔开。

```python
import random
for i in range(5):
    print(random.randint(1, 10))


```

import语句的另一种形式包括from关键字，之后是模块名称，import关键字和一个星号，例如from random import *。

使用这种形式的import语句，调用random模块中的函数时不需要random.前缀。但是，使用完整的名称会让代码更可读，所以最好是使用普通形式的import语句。

## 提前结束程序

通过调用sys.exit()函数，可以让程序终止或退出。因为这个函数在sys模块中，所以必须先导入sys，才能使用它。

```python
import sys

while True:
    print('Type exit to exit.')
    response=input()
    if response == 'exit':
        sys.exit()
    print('You typed ' + response + '.')
```

# 函数

```python
def hello():
    print('Howdy!')
    print('Howdy!!!')
    print('Hello there.')


hello()
hello()
hello()
```

def语句，定义了一个名为hello()的函数。def语句之后的代码块是函数体。这段代码在函数调用时执行，而不是在函数第一次定义时执行。函数之后的hello()语句行是函数调用。

```
Howdy!
Howdy!!!
Hello there.
Howdy!
Howdy!!!
Hello there.
Howdy!
Howdy!!!
Hello there.
```

## def语句和参数

略

## 返回值和return语句

略

## None值

在Python中有一个值称为None，它表示没有值。None是NoneType数据类型的唯一值。

## 关键字参数和print()

### end关键字

end关键字表示不换行。观察下面代码和运行结果。

```python
print('Hello')
print('World')

print('Hello', end='')
print('World')
```

```
Hello
World
HelloWorld
```

### step关键字

step关键字可以将打印的字符串按照step关键字指定的字符串进行拼接。观察下面的代码和结果。

```python
print('cats', 'dogs', 'mice')

print('cats', 'dogs', 'mice', sep=',')


```

```
cats dogs mice
cats,dogs,mice
```




