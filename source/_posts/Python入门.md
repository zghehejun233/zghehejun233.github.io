---
title: Python入门
description: Python入门知识笔记
categories: 编程
tags:
  - Python
abbrlink: 21062
header: ''
---

## 概述

### Python解释器原理

#### 传入参数

- 解释器读取命令行参数，把脚本名与其他参数转化为字符串列表存到 sys 模块的 argv 变量里。
- 执行 import sys，可以导入这个模块，并访问该列表。
  - 该列表最少有一个元素；
  - 未给定输入参数时，sys.argv[0] 是空字符串。
  - 给定脚本名是 '-' （标准输入）时，sys.argv[0] 是 '-'。
  - 使用 -c command 时，sys.argv[0] 是 '-c'。
  - 如果使用选项 -m module，sys.argv[0] 就是包含目录的模块全名。
- 解释器不处理 -c command 或 -m module 之后的选项，而是直接留在 sys.argv 中由命令或模块来处理。

### 运行环境

#### 字符编码

- 默认使用UTF-8

- 如果不使用默认编码，则要声明文件的编码，文件的 第一 行要写成特殊注释

```python
# -*- coding: encoding -*-
```

> Unicode和ASCII都懂</br>
> 为了把Unicode转化为可变长度的一种编码，产生了UTF-8编码。</br>
> UTF-8编码把一个Unicode字符根据不同的数字大小编码成1-6个字节，常用的英文字母被编码成1个字节，汉字通常是3个字节，只有很生僻的字符才会被编码成4-6个字节

## 数据类型及运算

> 所有整数默认视作int，浮点数视作float

首先要明确，Python并不是一个弱数据类型的语言。他只是有一个强大的类型推导机制，比如，可以在函数声明处使用`-> float`这样的语法规定返回值类型。

Python提供了五个标准数据类型，分别为：

1. Numbers
2. String
3. List
4. Tuple
5. Dictionary

### 整数

有一个很有意思的特性，Python中对于较长的数字可以使用下划线分割，如10000000> 100_0000_0

### 复数

- 使用a+bj或complex(a,b)来表示

### 字符串

#### 基本内容

- **单引号和双引号等价**，但实际运用中往往使用单引号比较多，反斜杠用于转义

- 字符串有“加（+）”连接和“乘(\*)”反复两种操作

- Python中的字符串默认使用str类型，其一个字符所对应的字节数是不确定的。在保存或传输时要转换成bytes类型。bytes类型使用b前缀来表明

- 交互式解释器会为输出的字符串加注引号，特殊字符使用反斜杠转义。

  > 虽然，有时输出的字符串看起来与输入的字符串不一样（外加的引号可能会改变），但两个字符串是相同的。如果字符串中有单引号而没有双引号，该字符串外将加注双引号，反之，则加注单引号。
  >
  > ```python
  > >>> 'doesn\'t'  # use \' to escape the single quote...
  > "doesn't"
  > >>> "doesn't"  # ...or use double quotes instead
  > "doesn't"
  > ```

- print() 函数输出的内容更简洁易读，它会省略两边的引号，并输出转义后的特殊字符

  ```python
  >>> print('"Isn\'t," they said.')
  "Isn't," they said.
  ```

- 如果不希望前置 \ 的字符转义成特殊字符，可以使用 原始字符串，在引号前添加`r`

  ```python
  >>> print('C:\some\name')  # here \n means newline!
  C:\some
  ame
  >>> print(r'C:\some\name')  # note the r before the quote
  C:\some\name
  ```

- 字符串字面值可以实现跨行连续输入。实现方式是用三引号："""...""" 或 '''...'''，字符串行尾会自动加上回车换行，如果不需要回车换行，在行尾添加 \ 即可

  ```python
  print("""\
  Usage: thingy [OPTIONS]
       -h                        Display this usage message
       -H hostname               Hostname to connect to
  """)
  ```

- python能够自动拼接两行字符串，不必使用链接符号；但合并变量和字面值必须使用

- 字符串索引，支持正负

  ```python
  word = 'Python'
  word[0]
  // 不存在-0索引，没有意义
  word[-2]
  ```

  > python没有char类型，只有长度为1的String

- 字符串切片，支持接受第三个参数：截取的布长

  ```python
  word[0:2]
  word[:2]
  word[4:]
  word[-2:]
  ```

  > 索引越界会报错，但切片会自动处理越界索引

#### 常用方法

- ord()和chr：编码转换

- encode()和decode()：将str编码或反编码为制定的bytes

  ```python
  >>> 'ABC'.encode('ascii')
  b'ABC'
  >>> '中文'.encode('utf-8')
  b'\xe4\xb8\xad\xe6\x96\x87'
  >>> '中文'.encode('ascii')
  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
  UnicodeEncodeError: 'ascii' codec can't encode characters in position 0-1: ordinal not in range(128)
  ```

  > decode()方法可以指定errors='ignore'来忽略错误的字节

- len()

- in：如果字符串中包含指定子串则返回True

- split()：给定一个字符串参数，将**实例分割为一个字符串数组**

- replace()：给定两个参数，用**第二个参数替换第一个参数**。还可以通过索引指定字符串的**某段**进行替换。

- strip()：返回去除两侧指定字符（默认为空格）的字符串

  > 相当于通过正负索引的遍历进行替换

#### 格式化字符串

占位符使用`{}`表示，通常配合`format()`方法实现字符串的组装

`format()`方法是字符串对象最常用的方法之一，可以用来替换占位符的内容，示例

  ```python
  urls = ['https://www.kugou.com/yy/rank/home/{}-8888.html?from=rank'
          .format(str(i))
              for i in range(1, 10)]
  ```

> 使用单行函数的形式写出非常pythonic的代码

### List

使用中括号括起的即是List。

Python的List应该是使用链表实现的（还没有考证）。

常用的方法：

- len()：
- append(element)
- insert(index,element)
- pop([index])
- cmp
- Max/min

#### 生成器

生成器是一种编程思想。他可以实现类似动态读取数据的效果，降低内存占用，算是用时间换空间的一种方式。

- 生成器可以实现数据的懒加载，缓解内存压力
- 一种获得方式是将通过循环得到的数组，中括号更改为小括号即可
- 另一种方式是通过yield关键字获得

#### `yield`关键字

- 使用yield关键字返回一个数据，得到的就是一个**生成器**
- 函数在执行到有yield关键字的内容时会结束执行

#### 元素的生成

- 调用`.next()`或者`._next_（）`方法
- 最后一个元素使用`.next()`方法会抛出StopIteration异常
- 为了避免异常的发生可以使用for循环遍历

### Tuple

Tuple可以理解为**静态数组**，他最大的特征就是静态不可变。

- 元组的元素不能被修改，**使用小括号表示**
- 应当使用del删除整个元组
- 如果可能，能用tuple代替list就尽量用tuple，降低运算压力和内存开销

### 字典（dict，其他语言中一般指map）

与各种各样的map类似，无非就是这些基本的方法

- clear和pop
- get：获取指定key，并在不存在时返回None或指定结果，**能够避免错误**

## 流程控制语句

### while

- 示例

  ```python
  #!/usr/bin/python
   
  count = 0
  while (count < 9):
     print 'The count is:', count
     count = count + 1
   
  print "Good bye!"
  ```

- 使用while...else结构，在while条件为false时执行else子块

### 多重循环

- 示例

  ```python
  for var1,var2 in zip(list1,list2):
  ```

### if

- 由于 python 并不支持 switch 语句，所以多个条件判断，只能用 elif 来实现

- 示例

  ```python
  >>> x = int(input("Please enter an integer: "))
  Please enter an integer: 42
  >>> if x < 0:
  ...     x = 0
  ...     print('Negative changed to zero')
  ... elif x == 0:
  ...     print('Zero')
  ... elif x == 1:
  ...     print('Single')
  ... else:
  ...     print('More')
  ...
  More
  ```

### for

- 示例

  ```python
  >>> # Measure some strings:
  ... words = ['cat', 'window', 'defenestrate']
  >>> for w in words:
  ...     print(w, len(w))
  ...
  cat 3
  window 6
  defenestrate 12
  ```

- Python的for迭代列表或字符串等任意序列

- 使用for循环修改集合的内容，应当遍历其副本或者创建一个新的集合

  ```python
  # Strategy:  Iterate over a copy
  for user, status in users.copy().items():
      if status == 'inactive':
          del users[user]
  
  # Strategy:  Create a new collection
  active_users = {}
  for user, status in users.items():
      if status == 'active':
          active_users[user] = status
  ```

- range函数能够遍历数字序列

  ```python
  >>> list(range(5, 10))
  [5, 6, 7, 8, 9]
  
  >>> list(range(0, 10, 3))
  [0, 3, 6, 9]
  
  >>> list(range(-10, -100, -30))
  [-10, -40, -70]
  ```

  > range() 返回对象的操作和列表很像，但其实这两种对象不是一回事。迭代时，该对象基于所需序列返回连续项，并没有生成真正的列表，从而节省了空间。
  >
  > 这种对象称为**可迭代对象 iterable**，函数或程序结构可通过该对象获取连续项，直到所有元素全部迭代完毕

### else子句

- 循环语句支持 else 子句；for 循环中，可迭代对象中的元素全部循环完毕时，或 while 循环的条件为假时，执行该子句；break 语句终止循环时，不执行该子句。

- 示例

  ```python
  >>> for n in range(2, 10):
  ...     for x in range(2, n):
  ...         if n % x == 0:
  ...             print(n, 'equals', x, '*', n//x)
  ...             break
  ...     else:
  ...         # loop fell through without finding a factor
  ...         print(n, 'is a prime number')
  ...
  2 is a prime number
  3 is a prime number
  4 equals 2 * 2
  5 is a prime number
  6 equals 2 * 3
  7 is a prime number
  8 equals 2 * 4
  9 equals 3 * 3
  ```

### pass语句

- **pass** 不做任何事情，一般用做占位语句

## 文件IO

### 输入与读取

#### `input()`和`raw_input()`

这两个函数用于从Terminal获取用户的输入。

input返回string，需要手动转换，如int()方法

#### `open()`

`open()`函数可以打开一个文件并建立file对象。

- 示例

  ```python
  file object = open(file_name [, access_mode][, buffering])
  ```

### `print()`

### `write`和`read`

### tell和seek

- Tell返回文件内的位置，seek可以改变到指定位置

## 函数

### 定义函数

- 示例

  ```python
  def functionname( parameters ):
     "函数_文档字符串"
     function_suite
     return [expression]
  ```

- 函数的第一行语句可以选择性地使用文档字符串—用于存放函数说明

- return[]表示结束，留空则返回None

### 调用函数

- 类型转换函数
- isinstance：数据类型检查

### 函数参数

#### 位置参数

- 调用函数时，传入的两个值按照位置顺序依次赋给指定参数

#### 默认参数

- 指定某一个未知参数的默认值

- 必选参数在前，默认参数在后

- 变化比较大、覆盖范围广的参数放在前面，相对普遍的参数放在后面并使用默认参数

- 默认参数必须指向不可变对象

  示例

  ```python
  def add_end(L=None):
      if L is None:
          L = []
      L.append('END')
      return L
  ```

#### 可变参数

- 定义可变参数和定义一个list或tuple参数相比，仅仅在参数前面加了一个`*`
- 同样的，传入参数时可以在list或tuple前加\*前缀作为可变参数传入
- 在函数内部，参数`numbers`接收到的是一个tuple，因此，函数代码完全不变。

#### 关键字参数

- 关键字参数允许你传入0个或任意个含参数名的参数，这些关键字参数在函数内部自动组装为一个dict

- 示例

  ```python
  def person(name, age, **kw):
      print('name:', name, 'age:', age, 'other:', kw)
  ```

### 装饰器

装饰器是一个类似Java中注解的语法特性。它允许对函数进行统一的前置和后置操作。

举个例子就可以

```python
def authorization(fn):
    def check_and_do(name):
        if name != "mofanpy":   # 鉴权
            print(name + " has no right!")
            return 
        res = fn(name)
        return res
    return check_and_do

@authorization
def outer1(name):
    print(name+" outer1")

@authorization
def outer2(name):
    print(name+" outer2")

@authorization
def outer3(name):
    print(name+" outer3")

outer1("mofanpy")
outer2("morgan")
outer3("mofanpy")
```

### 高阶函数

高阶函数的引入，主要为了实现函数式编程的编程范式。

#### map()

- 可以实现列表数据的逐个运算，并通过tuple()、list()等方法获得对应的运算结果

#### reduce()

- 用于实现列表数据和上次运算结果的复合关系

#### filter()

- 返回运算结果为True的元素，可以对数据进行过滤

#### sorted()

## 模块化开发

## 多任务处理

python中的多线程是伪多线程，因为存在GIL。
1、Python语言和GIL没有关系，只是因为历史原因在Cpython虚拟机(解释器)中难以移除GIL
2、GIL：全局解释器锁。每个线程在执行的过程都需要先获取GIL，保证同一时刻只有一个线程可以执行代码。
3、线程释放GIL锁的情况：在IO操作等可能引起阻塞的system call之前，可以暂时释放GIL，
但在执行完毕后，必须重新获取GIL，python3使用计时器(执行时间到达阈值后，当前线程释放GIL)
或python2,tickets计数达到100
4、Python使用多进程是可以利用多核CPU资源的
5、多线程爬虫比单线程性能有提升，是因为IO阻塞会自动释放GIL锁

### 多线程

- 使用threading模块

#### 创建线程

- 使用`threading.Thread(target,name)`来创建一个新的线程
- 其中，target指向的函数被称为该现成的回调函数
- `thread_name.start`用于启动这个新线程
- `thread_name.join`是一个阻塞式方法，表示在当前位置等待新线程结束后再继续执行主线程

#### 线程同步

> 由于每个线程在执行前都需要获取全局解释锁（Global Interpreter Lock,GIL），因此线程是交替执行的。每个线程执行一定量代码后就会释放GIL交给其他线程。
>
> 当多个线程共享一个进程的内存空间、同时修改一个全局变量，我们认为这种情况线程安全。

- Python提供了锁机制保证线程安全
- 在需要保护的代码前添加一行`lock.acquire()`，最后添加一行`lock.release()`即可

### 多进程

- 通常使用multiprocessing模块的Process进行进程管理，Linux下也可以使用fork之间创建子线程

#### 直接建立子进程

- 使用`multiprocessing.Process(target,args)`创建新进程
- 与线程的管理类似，提供了`.start()`和`.join()`方法

#### 通过Pool池建立子进程

- 使用`Pool(num)`创建一个能同时容纳num个进程的pool对象
- 调用pool对象的`.apply_async(target,args)`方法创建进程
- 在调用`.join()`方法之前需要使用`.close`方法关闭pool池防止加入新的进程

#### 进程间通信

> 与线程不同，进程之间是完全独立运行的，因此Python使用multiprocessing模块中的Queue来进行管理

- 建立一个`Queue`对象
- 使用`q.put()`和`q.get()`方法获取数据

#### 共享内存

#### 上锁

### 协程

> 协程与进程、线程都不同，他是一个由async关键字创建的异步函数

- 异步函数返回的不是函数执行的结果，而是一个协程对象，需要通过`.send()`方法触发函数执行
- 异步函数退出时会抛出异常，其返回值就包含在异常对象中，使用`e.value`来获取
- 使用await关键字可以阻塞自身，执行另一个异步函数

## 错误和异常

### 异常处理

- 使用try...except语句

- 示例

  ```python
  #!/usr/bin/python
  # -*- coding: UTF-8 -*-
  
  try:
      fh = open("testfile", "w")
      fh.write("这是一个测试文件，用于测试异常!!")
  except IOError:
      print "Error: 没有找到文件或读取文件失败"
  else:
      print "内容写入文件成功"
      fh.close()
  ```

- 支持finally语句

- 异常可以附带参数，习惯命名为Argument，通常包含详细的错误信息

- raise语句可以手动触发异常

  示例

  ```python
  def functionName( level ):
      if level < 1:
          raise Exception("Invalid level!", level)
          # 触发异常后，后面的代码就不会再执行
  ```

### logging模块

- 示例

  ```python
  import logging
  format = logging.Formatter('%{asctime}s - %{name}s - %{levelname}s - ',
                             '%{pathname}s - %{lineno}s: %{message}s',datefmt='%Y-%m-%d %H:%M:%S')
  
  sh = logging.StreamHandler()
  sh.setFormatter(format)
  
  logger = logging.getLogger('MyLog')
  logger.setlevel(10)
  logger.addHandler(sh)
  
  logger.info('content')
  ...
  ```

## OOP的实现

Python是一门完全支持OOP范式的语言。

### 类的定义

- 格式示例如下

  ```python
  class class_name:
  compose = ['var','var'] # 类变量
  def _init_(self): # 魔法方法，类似构造方法
  def function(self, var):
  ```

- 注意类内的每个方法都需要调用参数`self`

#### 实例属性

- 类变量中的属性可以直接引用，对于每个实例，可以在`.other`属性中创建实例属性

### 继承

- 继承示例如下

  ```python
  class A:
  compose = []
  
  class B(A):
  ```

## Pythonic Coding

- 序列生成字典

  ```python
  lst = [('a', 1), ('b', 2), ('c', 3)]
  // 使用循环🏪存储
  for k, v in lst:
    dic[k] = v
  // 字典推导式
  {k: v for k, v in lst}

- 对未指定的key将value设置为0，可以用于一些可选参数的处理

  ```python
  if key not in dic:
    dic[key] = 0
  // 
  dic[key] = dic.get(key,0)
  ```

- 交换key和value

  ```python
  dic = {'Python': 1, 'Java': 2}
  new_dic = {}
  for k, v in dic.items():
      new_dic[v] = k
      
  // 另一种写法，还是用推导式
  new_dic = {v: k for k, v in dic.items()}
  ```

- 使用字典保存一个序列数据，当key已经存在时添加新的值到对应序列末尾；否则直接进行初始化

  ```python
  lst = [('a', 1), ('b', 2), ('c', 3)]
  dic = {'a': [0]}
  
  for key, value in lst:
      if key in dic:
          dic[key].append(value)
      else:
          dic[key] = [value]
          
  // setdefault(key, default)会先判断key是否存在
  // 存在则返回dct[key]
  // 不存在则把dct[key]设为 [] 并返回。
  for (key, value) in lst:
      group = dic.setdefault(key, [])
      group.append(value)
      
  // 运行结果
  # dic：{'a': [0, 1], 'b': [2], 'c': [3]}
          
  ```

- 交换两个字典相同key对应的值

  ```python
  dic1 = {'Python': 1, 'Java': 2, 'C': 3}
  dic2 = {'Python': 3, 'Java': 2, 'C++': 1}
  
  new_dic = {}
  for k, v in dic1.items():
      if k in dic2.keys():
          new_dic[k] = v
          
  // 这里的dic1.keys() & dic2.keys()用到的就是 
  // keys()进行集合运算
  // items()同样可以进行集合运算。
  print({k: dic1[k] for k in dic1.keys() & dic2.keys()})
  
          
  // 运行结果
  # {'Python': 1, 'Java': 2}
  ```

- 使用`sorted()`函数快速排序

  ```python
  dic = {'a': 2, 'b': 1, 'c': 3, 'd': 0}
  lst1 = sorted(dic.items(), key=lambda x: x[0], reverse=False)
  # [('a', 2), ('b', 1), ('c', 3), ('d', 0)]
  lst2 = sorted(dic.items(), key=lambda x: x[1], reverse=False)
  # [('d', 0), ('b', 1), ('a', 2), ('c', 3)]
  print('按照键降序：', {key: value for key, value in lst1})
  print('按照值降序：', {key: value for key, value in lst2})
  
  # 按照键降序： {'a': 2, 'b': 1, 'c': 3, 'd': 0}
  # 按照值降序： {'d': 0, 'b': 1, 'a': 2, 'c': 3}
  ```

- 使用`sorted()`函数对序列中的多个字典排序

  ```python
  dict_list = [
      {'letter': 'B', 'number': '2'},
      {'letter': 'A', 'number': '3'},
      {'letter': 'B', 'number': '1'}
  ]
  
  # 按 letter 排序
  print(sorted(dict_list,
               key=lambda dic: dic['letter']))
  # 按 letter, number 排序
  print(sorted(dict_list,
               key=lambda dic: (dic['letter'], dic['number'])))
               
  # [{'letter': 'A', 'number': '3'}, {'letter': 'B', 'number': '2'}, {'letter': 'B', 'number': '1'}]
  # [{'letter': 'A', 'number': '3'}, {'letter': 'B', 'number': '1'}, {'letter': 'B', 'number': '2'}]
  ```
