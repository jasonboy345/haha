# 函数

## 函数概念
* 实现一定功能的代码段
* 复用性
* 函数三要素: `功能` `参数` `返回值`

### 内置函数

```python
# python2
import sys
dir(sys.modules['__builtin__'])

# python3
dir(__builtins__)
```

## 定义函数 

```python
def 函数名(参数1,参数2...):
    语句1
    语句2

```

* 数字符串中元素个数

```python
def char_count(str, char):
    return str.count(char)

char_count('American', 'a')
```

* 数任意字符串中字符个数

```python
#!/usr/bin/env python3

def char_count(str):
    char_list = set(str)
    for char in char_list:
        print(char, str.count(char))

if __name__ == '__main__':

    s = input("Enter a string: ")

    char_count(s)
```

> * 1 第一行 说明需要使用python3的解释器执行当前脚本
* 2 函数没有return return的就是none,函数中返回值和参数都是可选的
* 3 通过集合获得所有不重复的字符集
* 4 `if __name__ == '__main__':`相当于c语言的main函数,作为程序执行的入口,让`程序可以独立运行`,也可以`导入到其他程序中`

## 变量作用域


### 局部变量

```python
#!/usr/bin/env python3
def change():
    a = 90
    print(a)
a = 9
print("Before the function call ", a)
print("inside change function", end=' ')
change()
print("After the function call ", a)
```

> * `print(, end='\n')` end默认为一次输出后换一行 
`end:   string appended after the last value, default a newline.`
*  `print(, end = ' ')` 不换行
* 函数体内变量a为局部变量

### 全局变量


```python
#!/usr/bin/env python3
a = 9
def change():
    global a
    print(a)
print("Before the function call ", a)
print("inside change function", end=' ')
change()
print("After the function call ", a)
```

> * 变量a通过global变为全局变量 a在函数体内和函数体外都可以使用 


```python
#!/usr/bin/env python3
def change():
    global a
    a = 90
    print(a)
a = 9
print("Before the function call ", a)
print("inside change function", end=' ')
change()
print("After the function call ", a)
```
> * 使用global后函数体内的变量变成全局变量
* `局部变量: `函数体内定义的变量
* `全局变量: `函数体内使用global关键词修饰的变量
* `函数体外定义的变量函数体内也可以访问`
* `尽量不要使用global关键词,他是为了满足在函数体内定义全局变量的需要,其实是伪需求,在函数体内定义一个全局变量本来就很奇怪`


## 参数


### 顺序传参

```python
def subtract(a,b):
    print(a-b)

subtract(10,5)
subtract(5,10)
```


### 参数名传参
* 修改IP和端口号

```python
def connect(ipaddress, port):
    print("IP: ", ipaddress)
    print("Port: ", port)
# 默认顺序传参
connect('192.168.1.1', 22) 
# 错误顺序传参
connect(22, '192.168.1.1') 
# 参数名传递参数
connect(port=22, ipaddress='192.168.1.1') 
```

* 只允许使用参数名传参

```python
def hello(*, name="User"):
    print("hello", name)

# 报错typeerror
hello("nihao world")
# 只能使用参数名传递参数 
hello(name = "nihao world") 
```

### 默认值参数函数
```python
def connect(ipaddress, port=22):
    print("IP: ", ipaddress)
    print("Port: ", port)

connect('192.168.1.1', 2020) 
connect('192.168.1.1') 
```

* `注意`默认值参数只被赋值一次,因此如果默认值参数是可变对象(列表 字典 大多数类实例时)会有所不同

```python
def f1(a,data=[]):
    print(id(data))
    data.append(a)
    print(data,id(data))

print(f1(1))
print(f1(2))
print(f1(3))
# [1,2,3,4]
print(f1(4))


```
> * 因为`列表是引用类型` 
* python的变量有`引入类型和普通类型` 
* a = 123 这是`普通类型` 传参给函数的时候会`直接复制传值`
* `列表字典`等都是`引用类型` 传递给函数都`传递的是引用的地址,访问到原始值`



* 要避免以上结果

```python
def f2(a,data=None):
    print(id(data))
    if data is None:
        data = []
    data.append(a)
    print(data,id(data))

print(f2(1))
print(f2(2))
print(f2(3))

```


### 非关键词收集函数

* connect函数连接目标服务器的多个端口

```python
def connect(ipaddress, *ports):
    print("IP: ", ipaddress)
    print(type(ports))
    for port in ports:
        print("Port: ", port)

connect('192.168.1.1')
connect('192.168.1.1',22)
connect('192.168.1.1',22,23,24)

```


### 函数中修改参数值

* C语言中`传值`和`传引用`
* `不可变对象和可变对象` 相当于 `传值和传引用`
* 不可变对象 `数值 字符串 元祖`
* 可变对象 `列表 字典`

```python
#!/usr/bin/env python3

def connect(ipaddress, ports):
    print("IP: ", ipaddress)
    print("Ports: ", ports)
    ipaddress = '10.10.10.1'
    ports.append(8080)

if __name__=="__main__":
    ipaddress = '192.168.1.1'
    ports = [22,23,24]
    print("Before connect:")
    print("IP: ", ipaddress)
    print("Ports: ", ports)
    print("In connect:")
    connect(ipaddress, ports)
    print("After connect:")
    print("IP: ", ipaddress)
    print("Ports: ", ports)
```
> * 在函数体中改变`ipaddress`没有效果,因为他是`字符串不可变对象`
* 在函数体中改变`ports`有效果,因为他是`列表可变对象`



