# 文件处理
* 文件处理是项目开发中`数据持久化`和`获取配置信息`的主要方式
* 日常工作中遇到各种文件类型 `word 视频 文本`
* python中提供了`文件读写函数` 处理各种类型的文件


## 打开和关闭文件

* `open()`函数打开文件,返回一个文件对象,我们队文件的读写都使用这个对象
* `open(arg1,arg2)`第一个参数是`文件路径或文件名`，第二个是`文件的打开模式`
	* `r`,只读
	* `w`,读写
	* `a`,追加
	* `b`,二进制
	* 默认为只读的形式

```bash
# 打开文件
file = open('/etc/protocols')
# 查看文件对象类型
type(file)
# 查看文件
file
```

> * 程序结束后,需要关闭文件对象
* 不关闭会持续占用内存和操作系统资源,也可能造成数据丢失
* 使用`close()`关闭文件,重复关闭不会有任何影响

```bash
# 关闭
file.close()
# 查看文件
file
```

* 工作中一般使用with语句处理文件对象
* 文件用完后会自动关闭
* 发生异常也没关系,他是try-finally块的简写 

```python
with open('/etc/protocols') as file:
    count = 0
    for line in file:
        count += 1
    print(count)
```

> * 程序负责打印文件行数
* 代码块中没有close
* 代码执行到with代码块之外,文件会被自动关闭

## 读取文件内容

* `linux`中读取文件
```bash
cat 文件名.txt
```

* 文件 打开 读取 关闭

```python
# 文件路径
filename = '/路径/test.txt'
# 打开文件
file = open(filename)
# 读取文件
file.read()
# 关闭文件
file.close()
```

* 使用with操作文件读取

```python
filename = '/路径/test.txt'
with open(filename) as file:
    file.read()
```
> * 项目开发中谨慎使用`read()`读取整个文件,
* 因为你的系统内存可能不足以存储整个文件内容
* `read`执行一次后在执行不会有任何输出


* `readline()`文件读取函数
* readline()每次读取一行 
* readlines()一次读取所有行
* 返回的是一个列表 列表元素是字符串

```python
# 使用readline()读取文件内容
filename = '/路径/test.txt'
file = open(filename)
# 读取一行
file.readline()
# 读取一行
file.readline()
file.close()

# 使用readlines()读取文件内容
file = open(filename)
file.readlines()
file.close()
```

* for循环遍历文件对象,读取文件中的每一行

```python
file = open(filename)
for x in file:
    print(x, end = '')
file.close()

```

* 接受用户输入的字符串作为文件名
* 读取文件行数和文件内容

```python
#!/usr/bin/env python3

filename = input("Enter the file name: ")

with open(filename) as file:
    count = 0
    for line in file:
        count += 1
        print(line)
    print('Lines:', count)
```


## 写入文件
* `write()`打开文件,写入文本

```python
# 清空写方式打开
filename = '/路径/test.txt'
with open(filename, 'w') as file:
    file.write('test')
    file.write('testline')

# 查看写入
with open(filename, 'r') as file:
    file.readlines() 

# 追加写的方式打开
filename = '/路径/test.txt'
with open(filename, 'a') as file:
    file.write('test')
    file.write('testline')

# 查看写入
with open(filename, 'r') as file:
    file.readlines() 

```

## 拷贝文件
* 如`linux`中的`cp`命令

```python
#!/usr/bin/env python3

import sys

def copy_file(src, dst):
    with open(src, 'r') as src_file:
        with open(dst, 'w') as dst_file:
            dst_file.write(src_file.read())

if __name__ == '__main__':
    if len(sys.argv) == 3:
        copy_file(sys.argv[1], sys.argv[2])
    else:
        print("Parameter Error")
        print(sys.argv[0], "srcfile dstfile")
        sys.exit(-1)
    sys.exit(0)
```

> * `sys`模块,`sys.agv`包含所有命令行参数
* `sys.agv[0]第一个参数代表程序自身`

```python
#!/usr/bin/env python3

import sys
print("Program:", sys.argv[0])
print("Parameters:")
for i, x  in enumerate(sys.argv):
    if (i == 0):
        continue
    print(i, x)
```

> * 新函数 `enumerate(iterableobject)`,通过这个函数
* 在列表循环时,可以获得列表索引位置和对应的值
* 使用 `continue` 去除了 `sys.argv[0]` 程序自身


## 序列化
* 内存中的对象转化为可存储的格式
* python有两种方式进行序列化`pickle 模块`和`JSON格式`

### pickle模块
* 字典存到文件中,并且读取出来恢复为字典对象

```python
import pickle
courses = { 1:'Linux', 2:'Vim', 3:'Git'}
with open('./courses.data', 'wb') as file:
    pickle.dump(courses, file)

with open('./courses.data', 'rb') as file:
    new_courses = pickle.load(file)

new_courses

type(new_courses)

```
> * `写入和读取文件`都需要使用 `b 二进制模式`
* 只将对象序列化成一个字节流，那可以使用 `pickle.dumps(obj)`

### JSON
* `JSON` (`JavaScript Object Notation`, `JS 对象标记`)是一种`轻量级的数据交换格式`
* `JSON格式`在互联网应用开发中运用的非常广
* `不同的服务组件之间`进行数据传递的格式
* 互联网应用提供的`各种 API 接口返回值`基本都是 `JSON 格式`
* python有json模块 支持JSON序列化

```python
import json
courses = { 1:'Linux', 2:'Vim', 3:'Git'}
json.dumps(courses)
with open('courses.json', 'w') as file:
    file.write(json.dumps(courses))
with open('courses.json', 'r') as file:
    new_courses = json.loads(file.read())

new_courses

type(courses)

```

> * `dumps` 和 `loads` 分别执行了序列化和反序列化
*  `JSON 序列化后的内容为字符串`
* 文本`写入和读取` `不需要用二进制`


## 文件和文件夹操作
* `os.path`模块,获取和处理文件文件夹属性
	* 文件绝对路径		`os.path.abspath(path)`
	* 文件名 			`os.path.basename(path)`  
	* 文件路径 		`os.path.dirname(path)`  
	* 路径是否为文件 	`os.path.isfile(path)`  
	* 路径是否为目录 	`os.path.isdir(path)`  
	* 路径是否存在	 	`os.path.exists(path)` 
	* 目录路径和文件名合成一个路径 `os.path.join(path1[, path2[, ...]])` 

```bash
filename = '/路径/test.txt'
os.path.abspath(filename)
os.path.basename(filename)
os.path.dirname(filename)
os.path.isfile(filename)
os.path.isdir(filename)
os.path.exists(filename)
os.path.join('/路径', 'test.txt')
```




