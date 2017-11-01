# 面向对象

* 是一种`程序设计思想` 
* `面向过程思想: `设计程序 `程序一条条指令顺序执行`,当指令变得多起来时,他们被分割成`函数`
* `面向对象思想: ` `对象`视为程序的组成单元,程序执行通过`调用对象提供的接口`完成

## 面向对象核心
* 抽象
* 封装
* 继承
* 多态


## 面向过程
* “有一条叫旺财狗和一只叫 Kitty 的猫在叫，旺财发出 wang wang wang … 的叫声，Kitty 发出 miu miu miu 的叫声 …”

```python
def main():
    dog_name = '旺财'
    dog_sound = 'wang wang wang...'
    cat_name = 'Kitty'
    cat_sound = 'miu miu miu...'
    print(dag_name + ' is making sound ' + dog_sound)
    print(cat_name + ' is making sound ' + cat_sound)

main()

```

> * 以上为面向过程编程方法(代码风格)


## 抽象 类和实例
* 对特定实例`抽象出`共同的`特征和行为`

```
dog:
    name()  (特征)
    bark()  (行为)

cat:
    name()  (特征)
    mew()   (行为)   
```
> * `特征和行为`在程序语言中叫`属性(Attribute)和方法(Method)`


## 封装
* 封装 用类将`数据和对数据的操作`封装在一起,`隐藏内部数据`,`对外提供公共的访问接口`

```python
class Dog(object):
    def __init__(self, name):
        self._name = name
    def get_name(self):
        return self._name
    def set_name(self, value):
        self._name = value
    def bark(self):
        print(self.get_name() + 'is making sound wang wang wang...')

class Cat(object):
    def __init__(self, name):
        self._name = name
    def get_name(self):
        return self._name
    def set_name(self, value):
        self._name = value
    def mew(self):
        print(self.get_name() + 'is making sound miu miu miu...')


# 在 Python 实例化一个对象
dog = Dog('旺财')
cat = Cat('Kitty')
dog.bark()
cat.mew()

```
> * `object`是python中所有对象的祖先,是`所有类的基类`,python3中不是必须的,默认从object继承
* `__init__`是`初始化对象的各种属性`
* `self`代表`当前对象`


* 封装的好处 `提供访问控制,用户输入有大写有小写,我们统一对外提供首字母大写,可以在get_name中做访问控制`

```python
class Cat(object):
    def __init__(self, name):
        self._name = name
    def get_name(self):
        return self._name.lower().capitalize()
    def set_name(self, value):
        self._name = value
    def mew(self):
        print(self.get_name() + 'is making sound miu miu miu...')


# 在 Python 实例化一个对象
dog = Dog('旺财')
cat = Cat('Kitty')
dog.bark()
cat.mew()

```


## 继承和方法重写
* 狗猫 继承自Animal
* 父类 Animal

```python
class Animal(object):
    def __init__(self, name):
        self._name = name
    def get_name(self):
        return self._name
    def set_name(self, value):
        self._name = value
    def make_sound(self):
        pass
```
> * 使用`pass`直接略过函数,一个空函数必须有`pass`

* 狗猫 继承Animal

```python
class Dog(Animal):
    def make_sound(self):
        print(self.get_name() + ' is making sound wang wang wang...')


class Cat(Animal):
    def make_sound(self):
        print(self.get_name() + ' is making sound miu miu miu...')

dog = Dog('旺财')
cat = Cat('Kitty')
dog.make_sound()
cat.make_sound()

```

> * Dog 和 Cat `继承`了父类 Animal 的`构造方法`，`get_name` 和 `set_name`方法，并`重写`了父类的 `make_sound` 方法。


## 多态

* `同一方法`对`不同对象`产生`不同结果`

```python
animals = [Dog('旺财'), Cat('Kitty'), Dog('来福'), Cat('Betty')]
for animal in animals:
    animal.make_sound()
```

> * 不管 animal 具体是 `Dog 还是 Cat`(`不同对象`)，都可以在 for 循环中执行 `make_sound 这个方法`(`同一方法`)。这就是面向对象的`多态性`特征(`产生不同结果`)


## 其他

### 私有属性和方法
* java c php等语言中 规定 `private` 和 `protected`关键字修饰属性和方法
* 控制属性和方法`能否被外部或者子类`访问
* python中`约定`属性和方法前加`__`来拒绝外部访问
* 为什么是`约定`,因为不是绝对的私有,可以通过 `obj._Classname__privateAttribute' 'obj._Classname__privateMethod `
* 私有属性和方法`目的`外部使用者不要直接使用这个`私有属性或方法`


```python
class Shiyanlou: 
    __private_name = 'shiyanlou'
    def __get_private_name(self):
        return self.__private_name 

s = Shiyanlou()   
# 外部使用者不能直接使用私有属性
s.__private_name 
# 外部使用者不能直接使用私有方法
s.__get_private_name()  
# 外部使用者可以通过对象._类__私有属性名访问私有属性
s._Shiyanlou__private_name
# 外部使用者可以通过对象._类__私有方法名访问私有方法
s._Shiyanlou__get_private_name() 
```


### 静态变量和类方法

#### 静态变量 
* 动物都是`jack`养的,这个`owner`变量就是静态变量,一般在__init__之前

```python
class Animal(object):
    owner = 'jack'
    def __init__(self, name):
        self._name = name

# 可以通过Animal或者子类直接访问
print(Animal.owner)  # 'jack'
print(Cat.owner)  # 'jack'

```


#### 类方法
* 类方法和静态变量类似
* 类方法用 `@classmethd` 装饰
* 类方法中可以访问`类的静态变量`

```python
class Animal(object):
    owner = 'jack'
    def __init__(self, name):
        self._name = name
    @classmethod
    def get_owner(cls):
        return cls.owner


print(Animal.get_owner())  # 'jack'
print(Cat.get_owner())  # 'jack'
```

> * 类方法的第一个参数传入的是`类对象`，而不是实例对象，所以是 cls


### property
* 将方法变成属性来使用
* 实行 Python 风格的 `getter/setter` `获取属性 修改属性`
* 通过 property 获得和修改对象的某一个属性

```python
class Animal(object):
    def __init__(self, name):
        self._name = name
    @property
    def name(self):
        return self._name
    @name.setter
    def name(self, value):
        self._name = value
    def make_sound(self):
        pass

class Cat(Animal):
    def make_sound(self):
        print(self.get_name() + ' is making sound miu miu miu...')

# 访问属性的方式获取name
cat = Cat('Kitty')
print(cat.name)

# 访问属性的方式修改name
cat.name = 'katty'
print(cat.name)

```


### 静态方法
* 静态方法用 `@staticmethod` 装饰，和 `classmethod` 有点类似
* 静态方法访问时不需要实例参与



```python
class Animal(object):
    owner = 'jack'
    def __init__(self, name):
        self._name = name

# 静态方法
    @staticmethod
    def order_animal_food():
        print('ording...')
        print('ok')

# 类.静态方法
Animal.order_animal_food()

```

