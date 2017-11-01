# 基本语法

## 简介
### python是什么 

* 编程语言
* 丰富的基础模块和第三方模块 
* 这些模块包含`数据库`,`web开发`,`文件操作`;避免重复造轮子
* python版本,目前有python2和python3,相互不兼容,大部分库已经支持python3


### 优缺点

* 优点: 简单,`少量的代码实现复杂的功能`
* 缺点: 解释型的编程语言,每次执行的时候会一行一行的解释执行,执行的性能比不上编译型的语言,Python 程序的源代码完全开放。因为Python程序是脚本，不是编译成二进制分发的，通常很难进行代码保护。


### 应用场景

Python 最主要的应用场景包括网络爬虫，Web 开发，自动化运维，数据分析等领域


## 开发环境

### 安装

* Ubuntu

```bash
使用 apt-get 安装
sudo apt-get update
sudo apt-get install python3
```

* Mac

```bash
brew install python3
```

* Windows

```
Python 官网下载后通过图形界面一步步点击下一步进行安装
```


### 交互
* 终端中输入`python3`进入交互环境


### 执行脚本
* 直接使用python3解释器执行脚本

```bash
echo "print('hello world')" > /Users/wangsheng/hello world.py
python3 /Users/wangsheng/hello world.py
```

## 初次尝试
* 初次接触Python的`脚本编写与执行`、`模块引入和使用`



### 第一行

```bash
#!/usr/bin/env python3
```

*  `#!` Shebang
* 目的是告诉 shell 使用 Python 3 解释器执行其下面的代码

### 模块与引入

```python
from math import pi
```

* 从math库中引入 pi，让当前的文件中可以使用 pi


### 执行代码
* 用python3 命令指定脚本 python3 执行
* 直接执行脚本


```bash
要运行脚本文件 circle.py，还要为文件添加可执行权限
chmod +x circle.py
执行脚本
执行脚本的时候前面需要输入 ./ 表示在当前目录下的脚本
./circle.py
```


## 变量与数据类型
### 变量 
* 变量,编程语言中为了更好的处理数据
* 变量可以是不同的数据类型
* python中变量不需要声明可以直接使用

### 变量名
* 字母数字下划线
* 不能以数字开头
* 不能是关键词

```python
import keyword 
keyword.kwlist
```

### 基本数据类型
* 整型 
* 布尔 `True False`
* 浮点 
* None 代表未定义

### 使用变量及打印
* print() 打印输出
* type显示变量数据类型

### 运算
* 整型和浮点型混合运算中,整型会被转化为浮点型

### 字符串
* `+` 字符串连接
* `\` 字符串转义
* `:` 字符串切片 `字符串[起始位置:结束位置]`
* `len()` 字符串中字符数量

### 流程控制
#### 顺序结构
#### 分支结构

```python
if 条件语句1:
    输出1
elif 条件语句2:
    输出2
else :
    输出3
``` 

* input
* input获取用户输入
* input中的参数将输出到屏幕上
* 用户输入的内容会被函数返回,返回的值为字符串
* 如果不输入，程序将始终阻塞等待

```python
input("Please enter: ")
```

#### 循环结构
* for 循环主要用在依次取出一个列表中的项，对列表进行遍历处理

```python
for a in range(10):
    print(a)
```

* while

```python
w = 100
while w > 10:
    print(w)
    w -= 10
```

* 循环控制语句
* break表示停止当前循环
* continue表示跳过本轮循环

## 异常处理 

### 什么是异常
* 异常处理 `编程中必须要完成的内容`
* 不符合预期的`用户操作和数据输入`都会产生异常
* 处理异常是`保证程序稳定`的关键
* 异常出现原因很多,逻辑错误,用户输入错误都会造成异常

* 以下演示出现异常

```python
filename = input("Enter file path:")
f = open(filename)
print(f.read())
```

> 会出现文件不存在的异常，并且会发现 Traceback，这就是系统抛出的异常，异常的类型是 FileNotFoundError


* 最常见的异常类

```python
NameError 			访问一个未定义的变量
SyntaxError 		语法错误，这个严格讲算是程序的错误
IndeError 			对于一个序列，访问的索引超过了序列的范围（序列的概念会在后续讲到），可以理解为我的序列里只有三个元素，但要访问第4个
KeyError 			访问一个不存在的字典 Key，字典也会在后面详细讲到，Key 如果不存在字典就会抛出这个异常
ValueError 			传入无效的参数
AttributeError 		访问类对象中不存在的属性
```

### 异常处理
* 出现异常不可以直接抛给用户
* 应该使用python提供的`异常处理方法捕获`并且`处理异常`
* 处理方法 `try` `except` `finally`

```python
try:
    有可能抛出异常的代码
except 异常类型名称：
    处理代码
except 异常类型名称：
    处理代码

except可以有多个，每个处理不同类型的异常，也可以不写任何异常类型名称，则会处理所有捕获的异常
```


* 改进文件读取程序

```python
filename = input("Enter file path:")
try:
    f = open(filename)
    print(f.read())
    f.close()
except FileNotFoundError:
    print("File not found")
```


* finally关键字
* 进行清理工作,经常和 except 一起使用
* 正常还是异常,这段代码都会执行

```python
filename = '/etc/protocols'
f = open(filename)
try:
    f.write('shiyanlou')
except:
    print("File write error")
finally:
    print("finally")
    f.close()
```
> 以只读的模式打开了一个文件,尝试向文件中写入内容,会抛出异常,虽然异常，但仍然执行到了 finally 代码块

### 抛出异常
* `raise`希望在程序中抛出异常的时候使用

```python
格式 
raise 异常名称
抛出一个ValueError
raise ValueError()
```
> 外部可以使用 except ValueError: 捕获和处理异常 

### 异常处理逻辑
* 程序执行出现异常 or 自定义抛出异常 raise 异常
* 捕获异常

```python
try: 
    可能出现异常的代码 
except 异常名:
    处理异常
```


