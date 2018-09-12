## 字符串相关操作

### 一、python拼接字符串

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
