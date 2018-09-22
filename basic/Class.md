## 类
Python也是面向对象的语言。面向对象最重要的优点包括：封装、继承、多态。

类是对某一类事物的描述，是抽象的、概念上的定义，对象是实际存在的的，属于某一个类，是类的实例。

举例说明超类和子类：“鸟类”是一个非常通用的说法，就是一个超类，它具有很多子类。例如“百灵鸟类”就属于子类，子类相当于超类的子集。

### 创建一个类
`self`是对于对象自身的引用，对象属性可以在外部访问并修改。

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

### 特性、函数和方法
`self`参数不依赖于调用方法的方式，可以使用其他变量引用同一个方法。`greet`中引用对象中的`greet`方法。

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