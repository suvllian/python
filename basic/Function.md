## 函数

### 关键字参数和默认值
参数可以设置默认值，同时可以根据参数名称去传值，而无需通过指定位置传递参数。
``` python 
def hello(greeting='Hello', name='Demon'):
    print '%s, %s!' % (greeting, name)

hello()
# Hello, Demon!

hello(greeting='Hi')
# Hi, Tom!

hello(name='Tom')
# Hello, Tom!

hello('Hello', 'Demon')
# Hello, Demon!

hello(name='Demon', greeting='Hello')
# Hello, Demon!
```

### 收集参数及其逆过程
使用星号`*`可以将参数收集到元组中。使用`**`可以参数收集到字典中。
``` python
def print_params(*params, **dict):
    print params
    print dict

print_params(1,2,3,4, x=1,y=2)
# 1, 2, 3, 4)
# {'y': 2, 'x': 1}

def print_params(x,y,z=3, *params, **dict):
    print x,y,z
    print params
    print dict

print_params(1,2,3,4,5,6, foo=1,bar=2)
# 1 2 3
# (4, 5, 6)
# {'foo': 1, 'bar': 2}
```

在调用参数时使用星号`*`可以将元组分配到中。使用`**`可以字典分配到参数中。

``` python
def add(x,y):
    print x + y

tuple1 = (1,2)
dict1 = { 'x': 2, 'y': 3 }

add(*tuple1)
# 3
add(**dict1)
# 5
```

### 作用域
当局部变量和全局变量命名冲突时，使用globals函数可以获取全局变量的值。

``` python
x = 1
def add(x):
    print x + globals()['x']

add(2)
# 3
```

如果在函数内部将值赋予一个变量，它会自动变成局部变量，除非告知其python将其生命为全局变量。
``` python
x = 1
def change_global():
    global x
    x = x + 1

change_global()
print x
# 2
```

### 闭包
Python中也存在闭包。一个函数可以定义在另一个函数中，外层函数返回里层函数。返回的函数还可以访问它的定义所在的作用域。
``` python
def multiplier(factor):
    def multiplyByFactor(number):
        return number * factor
    return multiplyByFactor

double = multiplier(2)
print double(5)
# 10
```