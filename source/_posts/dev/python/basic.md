---
title: Python基础
date: 2013/02/14 11:11:11
tags: "Python"
---

# Python

## 第一个Python 程序

### 输入和输出


```python
print('Hello, world')
```


```python
input('input your name')
```


```python
print("%d * %d = %d" % (1024, 768, 1024 * 768))
```

<!-- more -->

## Python 基础

### 数据类型和变量


```python
print -1
print 0
print 1
print 100000000000000000000000
```

#### 整数


```python
# 八进制
print range(000, 010 + 1)

# 十进制
print range(0, 10 + 1)

# 十六进制
print range(0x0, 0xf + 1)

# 进制转换怎么做?
```

#### 浮点数


```python
print 0.1234567890

# 科学计数法
print 1.23e-4
print 1.23e5
```

#### 字符串


```python
print '123'
print "abc"
print """qaz"""
print '""'
print "\"\""

# r'' 表示转义字符为自身
print r"\"\""

# """ 多行 """
print """
123
456
789
"""
```

#### 布尔值


```python
# 与
print("{:5} and {:5} is {}".format( "True",  "True",  True and True))
print("{:5} and {:5} is {}".format( "True", "False",  True and False))
print("{:5} and {:5} is {}".format("False",  "True", False and True))
print("{:5} and {:5} is {}".format("False", "False", False and True))

# 或
print("{:5}  or {:5} is {}".format( "True",  "True",  True or True))
print("{:5}  or {:5} is {}".format( "True", "False",  True or False))
print("{:5}  or {:5} is {}".format("False",  "True", False or True))
print("{:5}  or {:5} is {}".format("False", "False", False or True))

# 非
print("{:5} not {:5} is {}".format("",  "True", not  True))
print("{:5} not {:5} is {}".format("", "False", not False))
```

#### 空值


```python
print None is None
print None is not None
```

#### 变量


```python
# 在Python中，等号=是赋值语句，可以把任意数据类型赋值给变量，
# 同一个变量可以反复赋值，而且可以是不同类型的变量，例如：
a = 123
print(a)
a = 'xyz'
print(a)
# 这种变量本身类型不固定的语言称之为*动态语言*，与之对应的是*静态语言*。
# 静态语言在定义变量时必须指定变量类型，如果赋值的时候类型不匹配，就会报错。例如Java是静态语言

# 定义一个变量，如下：
a = 'abc'
# Python解释器干了两件事情：
# 1. 在内存中创建了一个'ABC'的字符串；
# 2. 在内存中创建了一个名为a的变量，并把它指向'ABC'。

b = a
print(id('abc'), id(a), id(b))
# 发现他们的地址是一样的, 赋给其他变量一样

```

#### 常量


```python
# 在Python中，通常用全部大写的变量名表示常量：
PI = 3.1415926535897932384626
print(PI)
```

### 运算符和表达式

|表1|__运算符与它们的用法__|-|-|
|:---:|:---:|---|---|
|**运算符**|**名称**|**说明**|**例子**|
|&plus;    |加|两对象相加;对象可以是数字/字符(串)|3 + 5 = 8 ; 'a' + 'b' = 'ab'|
|&minus;   |减|两数字相减;取负数|5 - 3 = 2 ; -1 = -1|
|&ast;     |乘|两数字相乘;取重复N次字符串|2 &ast; 2 = 4 ; 'ha' &ast; 3 = 'hahaha'|
|&ast;&ast;|幂|返回xy|x = 2; y = 3; x ** y = 8;|
|&sol;     |除|两数字相除;两整数相除只会返回整数|5 / 2 = 2; 5.0 / 2 = 2.5; 5 / 2.0 = 2.5;|
|&sol;&sol;|除取整|两数字相除取整数部分|5 //2 = 2; 5.0 //2 = 2.0; 5 //2.0 = 2.0;|
|&percnt;  |除取余|两数字相除取余数部分|5 % 2 = 1; 5.0 % 2 = 1.0; 5 % 2.0 = 1.0;|
|&lt;&lt;  |左移|左移N个比特位|2 << 2 = 8; 10  -> 1000|
|&gt;&gt;  |右移|右移N个比特位|9 >> 2 = 2; 1001-> 10|
|&amp;     |按位与|-|-|
|&vert;    |按位或|-|-|
|&Hat;     |按位异或|-|-|
|&sim;     |按位翻转|x -> -(x+1)|-|
|&lt;      |小于|-|-|
|&gt;      |大于|-|-|
|&le;      |小于等于|-|-|
|&ge;      |大于等于|-|-|
|&Equal;   |等于|-|-|
|&ne;      |不等于|-|-|
|and       |布尔"与"|-|-|
|or        |布尔"或"|-|-|
|not       |布尔"非"|-|-|

|表2|__运算符优先级__|-|-|
|:---:|:---:|:---:|---|
|**运算符**|**描述**|-|-|
|lambda|Lambda表达式|-|-|
|or                 |布尔“或”|-|-|
|and                |布尔“与”|-|-|
|not x              |布尔“非”|-|-|
|in, not in         |成员测试|-|-|
|is, is not         |同一性测试|-|-|
|<, <=, >>=, !=, == |比较|-|-|
|&vert;             |按位或|-|-|
|^                  |按位异或|-|-|
|&                  |按位与|-|-|
|<<, >>             |移位|-|-|
|+, -               |加法与减法|-|-|
|*, /, %            |乘法、除法与取余|-|-|
|+x, -x             |正负号|-|-|
|~x                 |按位翻转|-|-|
|\**                |指数|-|-|
|x.attribute        |属性参考|_|self.name|
|x[index]           |下标|_|list[0]|
|x[index:index]     |寻址段|_|list[1:3]|
|f(arguments...)    |函数调用|_|f(args)|
|(expression, ...)  |绑定或元组显示|-|-|
|[expression, ...]  |列表显示|-|-|
|{key:datum, ...}   |字典显示|-|-|
|'expression, ...'  |字符串转换|-|-|


```python
print(" 9 /  3 = {}".format(9 / 3))

print(" 9 %  3 = {}".format(9 % 3))

# 除法
print("10 /  3 = {}".format(10 / 3))

# 取余
print("10 %  3 = {}".format(10 % 3))

# 地板除
print("10 // 3 = {}".format(10 // 3))
```

### 字符串和编码

### List和Tuple

| 操作 	| 方法                                       	| 描述                                                	| 说明                    	|
|------	|--------------------------------------------	|-----------------------------------------------------	|-------------------------	|
| 增   	| L.append(object)                           	| append object to end                                	| 在列表尾部追加对象      	|
| 增   	| L.insert(index, object)                    	| insert object before index                          	| 在index之前插入对象     	|
| 增   	| L.extend(iterable)                         	| extend list by appending elements from the iterable 	|                         	|
| 删   	| L.remove(value)                            	| remove first occurrence of value.                   	| 移除首次出现的value     	|
| 删   	| L.pop([index]) -> item                     	| remove and return item at index (default last).     	| 移除index位置的值       	|
| 改   	| L.sort(cmp=None, key=None, reverse=False)  	| stable sort *IN PLACE*                              	| 列表排序                	|
| 改   	| L.reverse()                                	| reverse *IN PLACE*                                  	| 颠倒列表                	|
| 查   	| L.count(value) -> integer                  	| return number of occurrences of value               	| 查询value出现次数       	|
| 查   	| L.index(value, [start, [stop]]) -> integer 	| return first index of value.                        	| 查询value首次出现的位置 	|

### Dict和Set

#### Dictionary
> Python 字典 setdefault() 函数和get() 方法类似, 如果键不存在于字典中，将会添加键并将值设为默认值。


```python
D = {'a': 1, 'b': 2, 'c': 3}
print D.get('a')
print D.get('b')
print D.get('c')
print D.get('d')
print D.setdefault('e', 'Not Found')
```


```python
D = {'a': 1, 'b': 2, 'c': 3, 'd': 4}
E = {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}

# 比较两个字典元素
print cmp(D, E)

# 计算字典元素个数，即键的总数。
print len(D)
print len(E)

# 输出字典可打印的字符串表示。
print str(D)
print str(E)

# 返回输入的变量类型，如果变量是字典就返回字典类型。
print type(D)
print type(E)

# dict.items()
# 以列表返回可遍历的(键, 值) 元组数组
print D.items()

# dict.keys()
# 以列表返回一个字典所有的键
print D.keys()

# dict.values()
# 以列表返回字典中的所有值
print D.values()

# dict.get(key, default=None)
# 返回指定键的值，如果值不在字典中返回default值
print D.get('a'), D.get('e'), D.get('f', 'Not Found')
print E.get('a'), E.get('e'), E.get('f', 'Not Found')

# dict.setdefault(key, default=None)
# 和get()类似, 但如果键不存在于字典中，将会添加键并将值设为default
print D.setdefault('e', 5)
print D
print D.get('e')
```


```python
# l = [0,'a','b','c','d','e','f']
# for index, item in enumerate(l):
#     print index

# for i in l:
#     print i
#     
    
d = {'a':0,'b':1,'c':2,'d':3,'e':4,'f':5}
for key in d:
    d[key] = d[key]+1

print d
```

### 条件语句

### 循环语句

## 函数

## 高级特性

### 切片

### 列表生成式


```python
# 列表生成式即List Comprehensions，是Python内置的非常简单却强大的可以用来创建list的生成式。
print([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
print(list(range(1, 11)))

# 上面的各元素平方该如何生成呢？
print([1 * 1, 2 * 2, 3 * 3, 4 * 4, 5 * 5, 6 * 6, 7 * 7, 8 * 8, 9 * 9, 10 * 10])

# 1.使用循环生成
L = []
for x in range(1, 11):
    L.append(x * x)
print(L)

# 2.使用列表生成式一行语句即可实现
print([x * x for x in range(1, 11)])

# 可以加上判断语句筛选需要的数据
print([x * x for x in range(1, 11) if x % 2 == 0])

# 使用多层循环, 生成全排列
print([m + n for m in 'ABC' for n in 'XYZ'])

# 将list中的字符串变小写
print([x.lower() for x in ['Hello', 'World', 'IBM', 'Apple']])

# 可以使用两个变量来生成list
d = {'x': 'A', 'y': 'B', 'z': 'C' }
print([k + '=' + v for k, v in d.items()])
```

### 生成器(generator)


```python
# 第一种创建generator的方法就是将列表生成式的中括号改为圆括号即可
L = [x * x for x in range(10)]
g = (x * x for x in range(10))
print(L)
print(g)
```


```python
print(next(g))
```

#### 斐波拉契数列(Fibonacci)


```python
# 斐波拉契数列(Fibonacci)，除第一个和第二个数外，任意一个数都可由前两个数
# 1 1 2 3 5 8
```

### 迭代器

## 函数式编程

### 高阶函数


```python
help(filter)
```


```python
def odd(x):
    return x % 2 != 0

L1 = [1,2,3,4,5,6,7,8,9]

filter(odd, L1)
```

## map & reduce
[MapReduce: Simplified Data Processing on Large Clusters](http://research.google.com/archive/mapreduce.html)

### map

<img src="./img/map.png" alt="map" title="map"/>

### reduce
``` javascript
[x1, x2, x3, x4].reduce(f) = f(f(f(x1, x2), x3), x4)
```


```python
def pow(x):
    return x * x


def add(x, y):
    return x + y


L1 = [1, 2, 3, 4, 5, 6, 7, 8, 9]
L2 = ['0', '1', '2', '3', '4']
print map(pow, L1)
print reduce(add, L1)
print reduce(add, L2)
```

### 返回函数

### 匿名函数


```python
def div(x, y):
    return float(x) / y if y != 0 else 'Infinity'
multiplier = lambda x, y: float(x) * y
print div(1, 0)
print multiplier(3, 6)
```

### 装饰器(Decorator)


```python
# -*- coding: utf-8 -*-
def now():
    return '2019-01-01'


# 函数也是一个对象，而且函数对象可以被赋值给变量，所以，通过变量也能调用该函数。
f = now
print f()

# 函数对象有一个__name__属性，可以拿到函数的名字：
print now.__name__
print f.__name__

# 如果要给函数增加功能应该如何实现呢?
```


```python
# -*- coding: utf-8 -*-
# 本质上，decorator就是一个返回函数的高阶函数。所以，我们要定义一个能打印日志的decorator，可以定义如下：
# 执行顺序应该是3 8 4 5 6, 最后返回function(*args, **kwargs)
def log(func):
    def wrapper(*args, **kwargs):
        print('call %s():' % func.__name__)
        return func(*args, **kwargs)

    return wrapper


def now():
    return '2019-01-01'


print log(now).__name__
print id(now)
print log(now)()
print


# 语法糖
@log
def now():
    return '2019-01-02'


print now.__name__
print id(now)
print now()

# 通过上面可以发现函数now的__name__变成了wrapper, 如何解决呢?
# 如果decorator本身需要传入参数应该如何实现呢?
```


```python
# -*- coding: utf-8 -*-
# 编写一个返回decorator的高阶函数
# 执行顺序为: 3 11 4 9 5 6 7, 最后返回function(*args, **kwargs)
def log(text):
    def decorator(function):
        def wrapper(*args, **kwargs):
            print('%s %s():' % (text, function.__name__))
            return function(*args, **kwargs)

        return wrapper

    return decorator


def now():
    return '2019-01-01'


print log('execute')(now).__name__
print id(log('execute')(now))
print log('execute')(now)()
print


# 语法糖
@log('execute')
def now():
    return '2019-01-02'


print now.__name__
print id(now)
print now()

# 通过上面可以发现函数now的__name__变成了wrapper, 如何解决呢?
```


```python
# -*- coding: utf-8 -*-
# 引入functools包解决此问题
import functools


def log(text):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            print('%s %s():' % (text, func.__name__))
            return func(*args, **kwargs)

        return wrapper

    return decorator


def now():
    return '2019-01-01'


print log('execute')(now).__name__
print id(log('execute')(now))
print log('execute')(now)()
print


# 语法糖
@log('execute')
def now():
    return '2019-01-02'


print now.__name__
print id(now)
print now()

# 在函数调用前后打印日志如何实现呢?
```


```python
# -*- coding: utf-8 -*-
def log(func):
    def wrapper(*args, **kwargs):
        print('begin call %s():' % func.__name__)
        print func(*args, **kwargs)
        print('end call %s()' % func.__name__)

    return wrapper


@log
def now():
    return '2019-01-01'


now()
```

### 偏函数

## 模块
* 一个目录里面存在\__init__.py就是一个包(package)
* 一个py文件就是一个模块(module)


```python
# import
# 当Python执行import module语句的时候，它在sys.path变量中所列目录中寻找sys.py模块
import sys
print(sys.argv)
print(sys.path)
print(sys.__name__)
print(__name__)
```


```python
# from ... import
# 一般说来，应该避免使用from..import而使用import语句，因为这样可以使你的程序更加易读，也可以避免名称的冲突。
from sys import argv
print(argv)
```


```python
# dir()
# 可以使用内建的dir函数来列出模块定义的标识符。
import sys
dir(sys)
```


```python
import subprocess
dir(subprocess)
```


```python
import multiprocessing
dir(multiprocessing)
```


```python
import threading
dir(threading)
```

### datetime


```python
from datetime import date
d = date(2018, 8, 9)
print d
print d.ctime()
print d.fromordinal(15000)
print d.timetuple()
print d.today()
```


```python
# datetiem是一个模块
import datetime
help(datetime)
```


```python
# 里面还有一个datetime类
from datetime import datetime

# 获取当前日期和时间
print(datetime.now())

# 获取指定日期和时间
print(datetime(2018, 1, 1, 12, 12, 12))

# 日期转时间戳

```

### time


```python
import time
help(time)
```


```python
import time
time.time()
```

### json


```python
import json
help(json)
```

### urllib


```python
import urllib
help(urllib)
```


```python
url = 'https://api.douban.com/v2/book/2129650'
```


```python
f = urllib.urlopen(url)
print(json.dumps(json.loads(f.read()), ensure_ascii=False, indent=4))
f.close()
```

> Deprecated since version 2.6: The urlopen() function has been removed in Python 3 in favor of urllib2.urlopen().


```python
import urllib2
help(urllib2)
```


```python
try:
    f = urllib2.urlopen(url)
    print(json.dumps(json.loads(f.read()), ensure_ascii=False, indent=4))
    f.close()
except urllib2.HTTPError, e:
    print(e.code, e.reason)
except urllib2.URLError, e:
    print(e.reason)
```

### 正则表达式


```python
import re
help(re)
```


```python
x = 15435627401
p = re.compile(r'^(\d{3})(\d{4})(\d{4})$')

# 查找
print("\n# findall")
r = p.findall(str(x))
print(r)

print("\n# finditer")
r = p.finditer(str(x))
print(r)

print("\n# match")
# re.match 尝试从字符串的起始位置匹配一个模式，如果不是起始位置匹配成功的话，match()就返回None。
# r = re.match('(\d{3})(\d{4})(\d{4})', str(x))
r = p.match(str(x))
print(r.group(), r.group(0), r.group(1), r.group(2), r.group(3))
print(r.groups())

print("\n# search")
# re.search 扫描整个字符串并返回第一个成功的匹配。
# r = re.search('(\d{3})(\d{4})(\d{4})', str(x))
r = p.search(str(x))
print(r.group(), r.group(0), r.group(1), r.group(2), r.group(3))
print(r.groups())

# re.match只匹配字符串的开始，如果字符串开始不符合正则表达式，则匹配失败，函数返回None；而re.search匹配整个字符串，直到找到一个匹配。

# 拆分
print("\n# split")
r = p.split(str(x))
print(r)

# 替换
print("\n# sub")
# Python 的 re 模块提供了re.sub用于替换字符串中的匹配项。
# r = re.sub(r'(\d{3})(\d{4})(\d{4})', r'\1-\2-\3', str(x))
r = p.subn(r'\1-\2-\3', str(x))
print(r)
```

## 面向对象编程


```python
class Person():
    def __init__(self, name):
        self.name = name

    def sayHello(self):
        print("Hello, I'm %s" % self.name)


p = Person('Jim')
p.sayHello()
```

## 错误、调试和测试

## I/O编程

## 进程和线程

### 多进程


```python
from multiprocessing import Process


def do_something(action):
    print("I'm %s!" % action)


p = Process(target=do_something, args=("running", ))
p.start()
p.join(timeout=None)

# 注意target的值就是待执行的函数，不是字符串。
# 这有毛用？
```

### 进程池


```python
from multiprocessing import Pool


def do_something(_id, _action):
    print("%2s: I'm %s!" % (_id, _action))


p = Pool()
for i in range(20):
    p.apply_async(do_something, args=(i, "running", ))

p.close()
p.join()
```

### 多线程


```python
import threading


def do_something(action):
    print("I'm %s!" % action)


t = threading.Thread(
    target=do_something, args=("running", ), name="Thread-A-01")
t.start()
t.join(timeout=None)
```
