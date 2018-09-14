## 异常处理

为了保证程序的健壮性，一定要考虑到程序的异常事件，并且对异常事件进行合理的处理。这个时候就需要进行了解下Python异常相关的知识。

>
Python用异常对象表示异常情况。遇到错误后，会触发异常。如果异常对象并未被处理或者捕捉，程序就会回溯终止执行。


可以使用一个类或者实例参数调用raise语句。使用类时，程序会自动创建类的一个实例。raise也可以将代码中的错误向外层抛出。
``` python 
>>> raise Exception
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
Exception
```

``` python
>>> raise Exception('something error')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
Exception: something error
```

### 自定义异常类
要确保新的类从Exception类继承（也可以从内建异常类继承）。

``` python
class CustomException(Exception):
    flag = False
    def calc(self, value):
        try:
            return 10/value
        except ZeroDivisionError:
            if self.flag:
                print 'Division by zero is illegal'
            else:
                raise

calculator = CustomException()
result = calculator.calc(0)
```

### 捕获异常
#### Basic usage(catch all exceptions):
``` python
try:
    x = input('enter the first number:')
    y = input('enter the second number:')
    print x / y
except ZeroDivisionError:
    print 'wrong second number'
```

#### catch multiple exceptions:
``` python
try:
    x = input('enter the first number:')
    y = input('enter the second number:')
    print x / y
except (SyntaxError, ZeroDivisionError, TypeError):
    print 'wrong second number'
```

#### access error information:
``` python
try:
    x = input('enter the first number:')
    y = input('enter the second number:')
    print x / y
except (SyntaxError, ZeroDivisionError, TypeError), e:
    print 'wrong second number'
    print e
```

#### 可以添加else语句，在没有错误情况的时候执行：
``` python
while True:
    try:
        x = input('enter the first number:')
        y = input('enter the second number:')
        print x / y
    except (SyntaxError, ZeroDivisionError, TypeError), e:
        print 'Invalid input, please try again.'
    else:
        break
```