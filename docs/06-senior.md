# 高级特性
* python中有些高级用法,熟悉后能极大的提高编程的效率和代码质量

## lambda匿名函数

```python
double = lambda x:x*2
double(5)

```
> * lambda是匿名函数
* 格式 `lambda 参数:参数处理[返回值]`
* 匿名函数不需要使用return
* lambda通常用在需要传入一个函数作为参数,并且这个函数只在这一个地方使用的情况下,匿名函数一般作为参数传递进去



## 切片 slice
* 切片用于获取一个序列(列表或元祖)或字符串的一部分,返回一个新的序列或字符串
* 列表 元祖 字符串都可以使用切片

```python
letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
letters[1:3]

#下标对应表 
 0  1  2  3  4  5  6
 a  b  c  d  e  f  g
-7 -6 -5 -4 -3 -2 -1

letters[1:-4]
letters[:4]
letters[4:]
copy = letters[:]
copy

```


## 列表解析 list comprehension
* 列表解析 又叫列表推导,提供了优雅的方式操作列表元素

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
# 获取 numbers 中的所有偶数
[x for x in numbers if x % 2 == 0]
[2, 4, 6, 8, 10]
# 对 numbers 的每个数求平方
[x * x for x in numbers]
[1, 4, 9, 16, 25, 36, 47, 84, 81, 100]
```
> * `列表解析式格式` [返回值 for x in 列表 if 判断条件]


## 高阶函数

* `map` `filter` `lambda` 
* 函数作为参数传递进去

* 上面例子中的操作可以借助高阶函数完成

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
f = filter(lambda x: x % 2 == 0, numbers)
m = map(lambda x: x * x, numbers)
for ff in f:
    print(ff)

for mm in m:
    print(mm)
```
* 使用高阶函数增加了`调用函数的开销`,时空效率不如列表解析


## 字典解析 dict comprehension
* 字典解析 ,提供了优雅的方式操作字典元素

```python
d = {'a': 1, 'b': 2, 'c': 3}
{k:v*v for k, v in d.items()}
```
> * 字典不能被迭代,需要使用字典方法`items()`把字典变成一个`可迭代对象`。


## 迭代器 
* `迭代`一个一个读取、操作对象
* `可迭代（Iterable)`可以用`for...in`迭代它的元素

* __列表是可迭代的__

```python
letters = ['a', 'b', 'c']
for letter in letters:
    print(letter)
```

* __迭代器__,用`next`函数不断的获得他的下一个值,迭代器返回 `StopIteration`异常
* 可迭代对象都可以通过 `iter` 函数去获取它的迭代器

```python
letters = ['a', 'b', 'c']
it = iter(letters)
next(it)
next(it)
next(it)
next(it)
```
> * `可迭代对象`,实现了`__iter__` 和 `__next__` 这俩个魔法方法
* `iter`和`next`函数实际是调用这两个魔术方法

* 上面例子的背后其实是这样

```python
letters = ['a', 'b', 'c']
it = letters.__iter__()
it.__next__()
it.__next__()
it.__next__()
it.__next__()

```

> * 总结 能被`for`循环访问的是`可迭代对象`
* 能被`next`函数获取下一个值的是`迭代器`


## 生成器
* 生成器是一个`迭代器`
* 生成器只能`被迭代一次`
* 每次迭代的元素不是像`列表元素`一样，`已经在内存中`
* 每迭代一次，它`生成一个元素`

```python
g = (x**x for x in range(1, 4))
print(g)
for x in g:
    print(x)
```
> * 和列表解析有点像，只不过使用的是`圆括号`
* 不同于列表可以反复迭代，再迭代这个迭代器，它不会打印元素，也不回报错
* __`生成器的好处`__,生成器不是把所有元素存在内存，而是`动态生成`的;当要`迭代的对象有非常多的元素`时，使用生成器能为你`节约很多内存`，这是一个`内存友好`的特性


## yield

## 装饰器
* 可以为函数`添加额外功能`,而`不影响函数主体功能`
* python中`函数是一等公民`
* 装饰器实现的基础,函数可以作为参数`传递给另一个函数`,函数可以作为`另一个函数的返回值`
* `装饰器`本质上是一个函数,他接受一个函数作为参数

```python
from datetime import datetime
def log(func):
    def decorator(*args, **kwargs):
        print('Function ' + func.__name__ + ' has been called at ' + datetime.now().strftime('%Y-%m-%d %H:%M:%S'))
        return func(*args, **kwargs)
    return decorator

@log
def add(x, y):
    return x + y

add(1, 2)
```
> * 123

## 总结
* `lambda`：匿名函数
* `切片`：序列和字符串的子序列
* `列表解析`：不用 for 也能操作列表元素
* `字典解析`：不用 for 也能操作字典元素
* `迭代器`：一个个读取元素的对象
* `生成器`：只能被迭代一次的迭代器
* `yield`：返回生成器的 return
* `装饰器`：对函数进行修饰