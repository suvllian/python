## 魔术方法
在Python中，有一些特殊的方法名，这些名字组成的集合包含的方法称为魔术方法。如果对象中实现了这些方法，那么这些方法会在特殊的情况会被Python调用，而不用去人为调用方法。

### 参考文章
* [Python 魔术方法 - Magic Method](http://python.jobbole.com/88367/)

### Basic usage
魔术方法比较好理解，所以直接通过实例去学习使用方法就可以了。

``` python
# -*- coding: utf-8 -*-

class TestClass:
    def __init__(self):
        ''' 初始化操作 '''

        print '调用了类的__init__方法'

        self.name = "testClass"
        self.dict = {}
        self.list = [1, 2, 3]

    def __len__(self):
        ''' 返回对象长度 '''

        print '调用了类的__len__方法'
        return 3

    def __getitem__(self, key):
        ''' 通过下标取值 '''

        print '调用了类的__getitem__方法'
        if key == -1:
            return self.name
        else:
            if key not in self.dict:
                return self.__missing__(key)
            return self.dict[key]

    def __missing__(self, key):
        ''' 当key不在dict中被调用 '''

        print '调用了类的__missing__方法'
        return "%s is not in dict" % key

    def __setitem__(self, key, value):
        ''' 设置对象的值 '''

        print '调用了类的__setitem__方法'
        self.dict[key] = value

    def __delitem__(self, key):
        ''' 删除对象的值 '''

        print '调用了类的__delitem__方法'
        del self.dict[key]

    def __getattr__(self, key):
        '''当访问对象不存在的属性时，调用此方法
        Usage: ClassTest().abc
        '''

        print '调用了类的__getattr__方法'
        return "class is not exists %s method" % key

    def __contains__(self, key):
        ''' not in or in 判断元素是否在其中
        Usage: if "1" in ClassTest()
        '''

        print '调用了类的__contains__方法'
        return key in self.list

    def __iter__(self):
        ''' 创建一个迭代器
        Usage: for i in ClassTest():
                 print i
        '''

        print '调用了类的__iter__方法'
        return iter(self.list)

    def __reversed__(self):
        ''' 反转列表
        Usage: or i in reversed(ClassTest()):
                 print i
        '''

        print '调用了类的__reversed__方法'
        return reversed(self.list)

    def __str__(self):
        '''用于处理打印实例本身的时候的输出内容,默认为对象名称和内存地址
        Usage: print ClassTest()
        '''

        print '调用了类的__str__方法'
        return "This is a Test Class for Python Magic Method"

    def __repr__(self):
        ''' 序列化对象
        Usage: repr(ClassTest())
        '''

        print '调用了类的__repr__方法'
        return repr(self.dict)

    def getName(self):
        return self.name


testObj = TestClass()
print '\n'

if 1 in testObj:
    print True
print '\n'

print testObj["a"]
print '\n'

for item in reversed(testObj):
    print item
print '\n'

for item in testObj:
    print item
print '\n'

print testObj.aaa
print '\n'

print repr(testObj)
print '\n'

print len(testObj)
print '\n'

testObj['a'] = 1
print '\n'

print testObj['a']
print '\n'

```

运行结果：

``` python
调用了类的__init__方法

调用了类的__contains__方法
True

调用了类的__getitem__方法
调用了类的__missing__方法
a is not in dict

调用了类的__reversed__方法
3
2
1

调用了类的__iter__方法
1
2
3

调用了类的__getattr__方法
class is not exists aaa method

调用了类的__repr__方法
{}

调用了类的__len__方法
3

调用了类的__setitem__方法

调用了类的__getitem__方法
1
```