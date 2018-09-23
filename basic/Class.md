## 类
Python也是面向对象的语言。面向对象最重要的优点包括：封装、继承、多态。

类是对某一类事物的描述，是抽象的、概念上的定义，对象是实际存在的的，属于某一个类，是类的实例。

举例说明超类和子类：“鸟类”是一个非常通用的说法，就是一个超类，它具有很多子类。例如“百灵鸟类”就属于子类，子类相当于超类的子集。

### 创建一个类
`self`是对于对象自身的引用，对象属性可以在外部访问并修改。

``` python
# -*- coding: utf-8 -*-

class Person:
    def setName(self, name):
        self.name = name

    def getName(self):
        return self.name

    def greet(self):
        print 'Hello ' + self.name

Tom = Person()
Tom.setName('Tom')
print Tom.getName()
# Tom
Tom.greet()
# Hello Tom
print Tom.name
# Tom
Tom.name = 'Jack'
print Tom.name
# Jack
```

### 类的命名空间
所有位于class语句中的代码都在特殊的命名空间中执行——类命名空间。这个命名空间可由类内的所有成员访问，类的定义其实就是执行代码块，类的定义区并不只限定只能使用def语句。

``` python 
class Counter:
    print 'define a class: Counter'
    member = 0
    def init(self):
        Counter.member += 1

c1 = Counter()
# define a class: Counter
c1.init()
print Counter.member
# 1
print c1.member
# 1

c2 = Counter()
# define a class: Counter
c2.init()
print Counter.member
# 2
print c2.member
# 2
```

上面代码里，在类的作用域定义了一个可供所有成员访问的实例变量，用来计算成员的数量。可以通过类名去访问，也可以通过实例访问。

``` python
c2.member = 'c2'
print c2.member
# 2
```

可以重写特性值，新的值会屏蔽类中的变量。（可类比JavaScript中的作用域链来理解）

### 特性、函数和方法
`self`参数不依赖于调用方法的方式，可以使用其他变量引用同一个方法。`greet`中引用对象中的`greet`方法。

``` python
greet = Tom.greet
greet()
# Hello Tom
```

python并不直接支持私有方式，为了让方法或者特性变成私有，只要在名字前面加上双下划线即可。

``` python
class Person:
    def setName(self, name):
        self.__name = name

    def __getName(self):
        return self.__name

    def greet(self):
        print 'Hello ' + self.__getName()

tom = Person()
tom.setName('Tom')

tom.__name
# ttributeError: Person instance has no attribute '__name'
tom.__getName()
# AttributeError: Person instance has no attribute '__getName'
tom.greet()
# Tom
```

但是在类的内部定义中，所有以双下划线开始的名字都被“翻译”成前面加上单下划线类名的形式。

``` python
class Person:
    def setName(self, name):
        self.__name = name

    def __getName(self):
        return self.__name

    def greet(self):
        print 'Hello ' + self.__getName()

tom = Person()
tom.setName('Tom')

print tom._Person__name
# tom
```

### 继承
#### 指定超类
``` python

class Filter:
    def init(self):
        self.blocked = []

    def filter(self, sequence):
        return [x for x in sequence if x not in self.blocked]

class SPAMFilter(Filter):
    def init(self):
        self.blocked = ['SPAM']

f = Filter()
f.init()
print f.filter([1,2,3])
# [1,2,3]

s = SPAMFilter()
s.init()
print s.filter(['SPAM', 'SPAM', 'test'])
# ['test']
```

在定义子类时指定超类，子类可以重写超类中的方法。

#### 检查继承
`issubclass `可以检查一个类是否是另一个类的子类。  
`__bases__ `属性可以获取已知类的基类。  
`isinstance `可以判断某个对象是否是一个类的实例。
`__class__`可以获取对象属于哪个类。
`hasattr`可以判断对象中是否存在某个方法或者属性。
`setattr `可以设置对象中的属性。
`__dict__`可以查看对象中所有存储的值。

``` python
print issubclass(SPAMFilter, Filter)
# True
print issubclass(Filter, SPAMFilter)
# False
print SPAMFilter.__bases__
# (<class __main__.Filter at 0x10459fb48>,)
print Filter.__bases__
# ()
print isinstance(s, SPAMFilter)
# True
print isinstance(f, SPAMFilter)
# False
print s.__class__
# __main__.SPAMFilter
print hasattr(s, 'init')
# True
print hasattr(s, 'blocked')
# True
print hasattr(s, 'value1')
# False
print s.__dict__
# {'blocked': ['SPAM']}
setattr(s, 'name', 'Test setattr')
print s.name
# Test setattr
print s.__dict__
# {'name': 'Test setattr', 'blocked': ['SPAM']}
```

#### 多个超类
python可以多重继承多个超类，子类不用做任何事，就可以继承超类的所有方法，称为多重继承。  
如果多个超类中有相同的方法，要注意一下超类的继承顺序，先继承的类中的方法会重写后继承的类中的方法。

``` python 
class Calculator:
    def calculator(self, expression):
        self.value = eval(expression)

class Talker:
    def talk(self):
        print 'My value is ', self.value

class TalkingCalculator(Calculator, Talker):
    pass

tc = TalkingCalculator()
tc.calculator('1+2')
tc.talk()
# My value is  3
print TalkingCalculator.__bases__
# (<class __main__.Calculator at 0x10190fb48>, <class __main__.Talker at 0x10190f390>)
```
	

