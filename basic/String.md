## 字符串相关操作

### 一、 字符串和编码
计算机只能处理数字，如果要处理文本，只能先把文本转换成数字。在计算机中用8比特（bit）表示一个字节（byte），一个字节能表示的最大整数是255。  

最早只有127个字符被编码到计算机中，包括大小写英文字母、数字和一些符号，这个编码表被成为`ASCII`编码。

中文至少使用两个字节进行编码，所以中国制订了`GB2312`编码，把中文编进去。

由此诞生`Unicode`编码，把所有语言都统一到一套编码中，就不会出现乱码问题。通常`Unicode`用两个字节表示一个字符。现代操作系统和大多数编程语言都支持`Unicode`。  

所有语言统一成`Unicode`编码，存在一个问题，如果书写语言全部是英文，`Unicode`编码比`ASCII`编码需要多一倍存储空间，所以需要把`Unicode`编码转换成“可变长编码”的`UTF-8`编码。用`UTF-8`编码可以节省存储空间。

一个中文字符经过`UTF-8`编码通常占用3个字节，1个英文字符只占1个字节。

在计算机内存中，统一使用`Unicode`编码，需要保存到硬盘或者需要传输的时候，就转化成`UTF-8`编码。
用记事本编辑文件时，从文件读取的`UTF-8`编码被转换成`Unicode`字符到内存中，编辑完成后，保存时再把`Unicode`转换成`UTF-8`保存到文件。   
浏览网页时，服务器会把动态生成的`Unicode`内容转换成`UTF-8`再传输到浏览器。

* `ord()`：获取字符的整数表示。
* `chr()`：把编码转换成对应的字符。
* `len()`：计算字符串包含多少字符。
* `encode()`：字符串编码。
* `decode()`：字符串解码。

#### Basic usage

``` python
>>> ord('a')
97

>>> chr(97)
'a'

>>> 'abc'.encode('ascii')
abc

>>>len('中文')
6
```

Python源代码也是一个文本文件，所以当源代码中包含中文的时候，在保存源代码时，就需要务必指定保存为`UTF-8`编码。当Python解释器读取源代码时，为了让它按`UTF-8`编码读取，我们通常在文件开头写上这两行：

``` python 
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
```

#### 占位符

| 占位符 | 替换内容 |
| --- | --- |
|%d | 整数 |
|%f | 浮点数 |
|%s | 字符串 |
|%x | 十六进制整数|

#### format()
``` python
>>>'hello,{0},I am {1}'.format('carol', 'demon')
'hello,carol,I am demon'
```

### 二、python拼接字符串

#### 1.直接连接，中间有无空格均可
``` python
>>> print 'learn' 'python'
learnpython
```

#### 2.'+'连接
``` python
>>> print 'learn' + 'python'
learnpython
```

#### 3.','连接，输出中间会有空格
``` python
>>> print 'learn','python'
learn python
```

#### 4.格式化
``` python
>>> print 'learn %s' %'python'
learn python
>>> print '%s %s ' % ('learning', 'python') + 'makes me very happy'
learning python makes me very happy
```

#### 5.join连接
``` python
>>> print ' '.join(['learn','python' ])
learn python
>>> print ','.join(['learn','python' ])
learn,python
```

#### 6.format方法
``` python
>>> string = '{} {} {}'
>>> print string.format('today', 'is', 'Wednesday')
today is Wednesday
```

可以指定参数位置

``` python
>>> string = '{1} {2} {0}'
>>> print string.format('Wednesday', 'today', 'is')
today is Wednesday
```

#### 模版字符串
``` python 
# -*- coding: utf-8 -*-

from string import Template

str1 = Template('$x, I am Demon')
print str1.substitute(x='Caroline')

# 替换单词的一部分，必须用括号括起来
str2 = Template('Today is Mon${day}')
print str2.substitute(day='day')

# 使用$$插入美元符号
str3 = Template('$$ is a good $x')
print str3.substitute(x='thing')

# 可以使用字典提供值/名称对
str4 = Template('$x is very $y')
argv = {}
argv['x'] = 'learning'
argv['y'] = 'interesting'
print str4.substitute(argv)
```

### 三、字符串方法
#### find(sub_string, start_position, end_position)
可以在字符串中寻找子串，返回子串所在位置的最左端索引，没找到就返回-1
``` python
str = 'I am Demon'
print str.find('Demon')
# 5
print str.find('Demon', 1, 4)
# -1
print str.find('test')
# -1
```

#### split(sign)
根据分隔符讲字符串分割成序列
``` python
print 'abcde'.split()
# ['abcde']
print 'a b c d e'.split()
# ['a', 'b', 'c', 'd', 'e']
```

#### join(list)
需要被连接的序列元素必须是字符串
``` python
print ' '.join(['I', 'am', 'Demon'])
# I am Demon
```

#### lower()
返回字符串的小写形式
``` python
print 'TEST'.lower()
# test
```

#### upper()
返回字符串的大写形式
``` python
print 'test'.upper()
# TEST
```

#### replace()
返回字符串所有匹配项被替换后的字符串
``` python
print 'This is a test'.replace('is', 'not')
# Thnot not a test
```

#### strip(sign)
去除两侧的空格字符串，可以指定去除的符号，但是只会取出字符串两侧的，字符串中间包含的字符不会删除。
``` python
print '    abc   '.strip()
# abc
print ' *   !!! ****  a  *  bc  *****    !!!!'.strip(' *!')
# a  *  bc
```

#### title()
返回字符串的首字母大写形式
``` python
print 'test'.title()
# Test
```

#### isupper、islower、istitle
``` python 
print 'aB'.isupper() # False
print 'a'.isupper() # Flase
print 'aB'.islower() # False
print 'Alibaba'.istitle() # True
```