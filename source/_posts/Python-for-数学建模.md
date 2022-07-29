---
title: Python  科学计算
description: 用于简单科学计算和数学建模的Python知识
categories: 编程
tags:
  - Python
  - 数学建模
abbrlink: 23478
date: 2022-01-09 10:29:00
update: 2022-01-29 11:42:32
---

# 前言

- ![image-20220109215625112](https://tva1.sinaimg.cn/large/008i3skNly1gy7rk65f1qj310i09cack.jpg)
- https://www.zhihu.com/people/youcans-24/columns

# 数据处理

## 数据的存储

- 详见Python爬虫一文

## 文件管理

- 使用Python提供的os模块

### 文件和目录列表

- 使用`.listdir()`方法获得目录列表

### 目录操作

### 文件操作

- rename()：文件重命名

## 数据清洗

### 存储在数据库中的数据

- 优先考虑使用SQL语句进行清洗

### 存储在csv、xlsx文件中的数据

- 可以先使用可视化工具进行标准化处理

### 存储在XML、JSON和csv等文件中的数据

- 使用Python强大的字符串处理能力，使用`.split()`和`.strip()`等方法进行字符串的整理
- 使用正则表达式处理数据

# Numpy

## 简介

- Numpy主要加强了Python的数组运算能力，引入ndarray对象和ufunc函数，大大提高了Python的矩阵运算能力
- 基本模仿Matlab的风格，并实现了相似的矩阵保存和运算功能

## 数组对象

### ndarray

- ndarray被设计用来表示矩阵，通常被叫做数组
- 数组的维度成为轴，维度内元素的数量成为轴的长度

#### 数组的属性

- ndarray.ndim：返回维度数
- ndarray.shape：返回一个元组，表示数组的形状，其长度和维度相等，每个元素是对应维度的大小
- ndarray.size：数组元素的总个数
- ndarray.dtype：
- ndarray.itemsize：
- ndarray.data

#### numpy扩展数据类型

#### 数组的创建

- 直接创建

- 特殊数组的创建

  - empty()：建立一个空矩阵，随机生成元素
  - zeros()/ones()：生成0/1矩阵

  - .arange：与Matlab类似，可以接受四个参数，分别是start、end、step和dtype
  - .linspace：创建一个等差数列一维数组
  - .logspace：创建一个等比数列一维数组
  - numpy.random.rand/randn/randint：生成符合一定规律的随机矩阵
  - formfunction()：根据指定函数生成矩阵

## 数组操作

### 运算

- numpy使用@来表示矩阵乘法

### 获取数组内容

- numpy可以使用`···`来表示剩余轴
- 对于多维数组的迭代仅仅是针对第一个轴进行的，要想遍历全部，需要调用数组的`.flat`属性

### 修改数组内容

- .delete()：删除一行or一列数据
- .append()：插入数据

### 修改数组形状

- .reshape()、.ravel()和.resize()：重整数组形状，生成行向量，以及在原数组基础上进行重构（不建立新对象）

  > 特别的，`reshape()`方法接受类似（1，-1）、（2，-1）和（-1,1）这样的参数，将会得到一行、两行或者一列数据

- .T：转置变换 

- .flatten()：返回一份数组拷贝，相当于矩阵的行向量，接受一个order参数，提供以下选项

  | order | 含义                   |
  | ----- | ---------------------- |
  | C     | 按行顺序               |
  | F     | 按列顺序               |
  | A     | 原顺序                 |
  | K     | 元素在内存中出现的顺序 |

- .vstack()、.hstack()和.column_stack()：分别在垂直、水平和更高维度上进行数组的堆叠

  > `.c_`和`.r_`具有相同的作用

- .vsplit()、.hsplit()和.array_split()分别进行垂直、水平和自定义的拆分

## 高级索引

### 数组索引

- 使用`np.array()`方法建立一个numpy数组，可以实现从第一个维度开始的索引
- 使用一个高维数组对目标数组进行一维的索引，可以提升若干个维度
- 一维索引数组，可以获取目标数组的一维数据；二位索引数组，可以将若干个一维数据再进行组合，以此类推

### 布尔索引

- 使用一个与原始数组形状相同的布尔数组进行筛选

#### ix()索引

## linalg模块

### .linalg.norm

- 用于获得欧几里得范数
- 说白了就是两点间距离



# Pandas

## 简介

- 最早作为金融数据分析工具开发，有很强大的数据分析能力
- 支持类似SQL语句的模型

# Scipy

# Sympy

# Matplotlib入门

# Seaborn入门
