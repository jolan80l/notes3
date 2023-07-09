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




