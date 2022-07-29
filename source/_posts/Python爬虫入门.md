---
title: Python爬虫入门
description: Python爬虫的简单知识
categories: 编程
tags:
  - Python
  - 爬虫
abbrlink: 28509
date: 2022-02-08 10:29:00
updated: 2022-02-09 21:24:00
---
# 爬虫基本原理

## 网页构造

### 前端简述

- 前端开发最基本的是HTML、CSS和JavaScript，还有VUE等现代框架
- HTML用于描述网页的内容，爬虫需要获取的信息往往就在html标签或文本里
- 有时网站的内容直接显示，有时则会通过js显示，就很蛋疼

## 爬虫工作流程

### 基本的网络知识

- 网络连接最基本的工作就是发出一条request和一条response
- request需要一条url，他不仅有一条域名，还包含header和属性等等
- 服务器通过header鉴别请求发出者是不是个人，cookie用来存放身份信息，等等

### 常用的python库

- 常用的第三方库一般有Requsts（用于发起网络请求）和BeautifulSoup（用于解析response），以及scrapy框架

### url的构建

- 对于多页面的网站，通常可以通过观察，使用占位符和`.format()`方法构建一个url列表
- 有时相信内容的url会在标签的文本内，有时会在属性的href标签内，分别通过`.get_text()`和`.get('tag')`来获取

### 请求内容的解析

- bs4支持多种解析器，建议使用的是lxml（基于C）

# 简单爬虫程序

```python
import requests
from bs4 import BeautifulSoup
import time

# 请求头内容
headers = {
    'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) '
                  'Version/15.2 Safari/605.1.15'
}


def get_info(url):
    print('********* Start Analysing ********\n')
    print(url)
    res = requests.get(url, headers=headers) # 获取网站信息
    soup = BeautifulSoup(res.text, 'lxml') # 使用bs4解析
    ranks = soup.select('span.pc_temp_num') # 使用selector获取目标内容
    titles = soup.select('div.pc_temp_songlist > ul > li > a')
    for rank, title in zip(ranks, titles): # 多重循环进行遍历，构造字典
        data = {
            'rank': rank.get_text().strip('\t'), # 使用strip()方法除去空余内容
            'singer': title.get('title').split(' - ')[0], # 使用.split()方法分割符合的内容
            'song': title.get('title').split(' - ')[1]
        }
        print(data)


if __name__ == '__main__':
    urls = ['https://www.kugou.com/yy/rank/home/{}-8888.html?from=rank'.format(str(i))
            for i in range(1, 10)] # 构造url列表
    for url in urls:
        get_info(url)
        time.sleep(1) # 每次请求等待1s，防止被ban
    print('Finish.')

```



# 网络请求

## Request库使用示例

- 示例

  ```python
  import requests
  
  # header用来提供浏览器信息
  headers = {
  		'User-Agent': 'content'
  }
  
  web_data = requests.get('url',headers = headers)
  ```

## Request库的常用函数

### GET请求

- 使用`requests.get(url,headers)`方法发送GET请求并返回一个字符串实例

### POST请求

# 请求内容的解析

## bs4库示例

## bs4库常用函数

### 元素的查找

- find()：返回第一个符合匹配条件的元素

- find_all()：返回所有符合条件的元素

  > 以上两个函数主要接收tag、attibutes和attrs三个参数，其中attrs参数接受一个字典

- select()：通过选择器寻找元素

  > 对于nth-child(1)这样的内容，需要修改为nth-of-type(1)
  >
  > 对于li:nth-child(1)这样的序列，可以改为li实现遍历，此时返回的对象是一个数组

### 信息的获取

- get_text()：主要获取文本内容
- get()：获取标签内的内容

# 正则和re模块

## 正则表达式

### 一般字符

| 字符  | 含义                     |
| ----- | ------------------------ |
| .     | 匹配单个任意字符         |
| \     | 转义字符                 |
| [...] | 匹配集合中的任意一个字符 |

### 预定义字符集

| 字符 | 含义                                               |
| ---- | -------------------------------------------------- |
| \d   | 任意一个数字字符                                   |
| \D   | 任意一个非数字字符                                 |
| \s   | 任何空白字符，如空格、制表符等（等价于\f\n\r\t\v） |
| \S   | 任何非空白字符                                     |
| \w   | 任何单词字符，包括大小写字母和数字                 |
| \W   | 任何非单词字符                                     |

### 数量词

| 字符 | 含义 |
| ---- | ---- |
|      |      |
|      |      |
|      |      |
|      |      |
|      |      |
|      |      |
|      |      |
|      |      |



### 边界匹配

|      |      |
| ---- | ---- |
|      |      |
|      |      |
|      |      |
|      |      |

### 爬虫常用匹配

#### (.\*?)

- ()表示括号的内容作为返回结果

- .\*?是非贪心算法，匹配任意字符

- 示例

  ```python
  import re
  str = 'xxIxxxxxloxxxvxxexxxxxpyxxthonxx'
  info = re.findall('xx(.*?)xx',str)
  ```

## re模块

### search()

- 匹配并返回第一个符合要求的内容，返回正则表达式对象
- 接收三个参数，分别是pattern、string和flags。其中flags标志位用来控制匹配选项
- 要将正则表达式对象转为普通对象，使用`.group()`方法

### sub()

- 用于替换符合条件的匹配项
- 接受五个参数，分别为pattern、repl、string、count和flag。其中count是替换的最大次数，0表示替换所有；flags为标志位

### findall()

- 匹配所有符合要求的内容，返回一个列表

### 修饰符

| 修饰符 | 描述 |
| ------ | ---- |
| re.I   |      |
| re.L   |      |
| re.M   |      |
| re.S   |      |
| re.U   |      |
| re.X   |      |

- 其中常用的是`re.S`能够实现换行匹配

# Lxml库与Xpath

- Lxml使用Xpath语法对XML进行解析，是基于C的libxml2的Python封装

## 使用Lxml解析HTML

- 主要使用etree库

### 常用方法

- etree.HTML()/etree.parse()：解析HTML文件，返回element对象
- etree.tostring：输出解析的element对象

## Xpath语言

### 节点概念

### 节点选择

- 节点选择

| 表达式   | 描述                           |
| -------- | ------------------------------ |
| nodename |                                |
| /        | 根节点                         |
| //       | 当前节点的所有符合条件的子节点 |
| .        | 当前节点                       |
| ..       | 当前节点的父节点               |
| @        | 选取属性                       |

- 谓语

| 表达式          | 描述                                    |
| --------------- | --------------------------------------- |
| [n]             | 第n个元素（多个元素从1而不是0开始排列） |
| [@attribute]    | 含有指定属性的元素                      |
| [@attribute=''] | 属性为某特定值                          |

### 技巧

- /text()：获取标签中的文字信息

- 切片索引：将返回的数组转换为字符串

- starts-with：获取多个标签内容，示例

  ```python
  from lxml import etreee
  html = '''
  <li class='tag-1'>content1</li>
  <li class='tag-2'>content2</li>
  <li class='tag-3'>content3</li>
  '''
  selector = etree.HTML(html)
  contents = selector.xpath('//li[starts-with(@class,"tag")]/text()')
  for content in contents:
  	print(content)
  ```

- .string()：用于获取嵌套字符串的信息并保留父子关系，示例

  ```python
  from lxml import etreee
  html = '''
  <div class="red">content1
  		<h1>content2</h1>
  </div>
  '''
  selector = etree.HTML(html)
  content1 = selector.xpath('//div[@class="red"]')[0]
  content2 = content1.xpath('string(.)')
  ```

  

# API的使用

## API简介

- 不必多说
- 参阅API文档

## JSON解析

- 使用json库，将JSON解析为Python字典、数组和字符串，非常好使

### 常用方法

- json.loads()：解析JSON
- jsonElement.get()：获取信息
- pprint.pprint()：格式化打印json数据

# 数据存储

## txt文件

## csv文件

- 示例

  ```python
  import csv
  fp = open('file')
  writer = csv.writer(fp) # 创建writer实例
  ```

- 常用方法

  - .writerow('key':'value')：

- 可能需要修正编码格式

## xlsx文件

- 示例

  ```python
  import xlwt
  book = xlwt.Workbook(encoding='utf-8') # 创建工作簿
  sheet = book.add_sheet('Sheet1') # 创建工作表
  sheet.write(row,column,'value') # 写入数据
  sheet.save('filename')
  ```

  

## MongoDB存储

- MongDB是一种文档型数据库，NoSQL还包含键值存储型数据库（Redis）、列存储数据库（Hbase）和图形数据库（Graph）

## MySQL存储

# 多线程爬虫

- 示例

  ```python
  from multiprocessing import Pool
  if __name__=='__main__':
  		pool = Pool(processes=4)
  pool.map(get_info,rest_urls)
  ```

  

# 异步加载网页

- 主要通过抓取XHR信息获取url来实现

# 表单交互与模拟登录

## POST请求

### POST的使用

- 构造一个字典存储属性，并在请求时以data字段加入，示例

  ```python
  param = {
  	'key':'value',
  	'key':'value'
  }
  web_data = requests.post(url,data=param)
  ```

### 网页表单的提交

- 所有表单都在dorm标签内
- form标签有两个重要属性，分别是提交的URL，action和提交的字段，input
- 提交表单后，可以根据登录状态进行判断是否成功

## Cookie与模拟登录

# Selenium模拟浏览器

# Scrapy框架

## 框架基本使用

### 简介

#### 主要组件及其功能

- Scrapy Engine
- Spiders：实体类，用于提取网页数据，用“item”表示
- Item Pipeline：用于处理Spiders抽取的实体，进行数据处理

#### 目录结构

- spiders：具体的爬虫程序
- items.py：存放实体类，继承自`scrapy.Item`
- middlewares.py：
- pipelines.py：用于处理数据
- settings.py：框架配置，比如添加header、修改请求速度等
- scrapy.cfg：项目配置

### 数据处理

### 数据存储

### 辅助功能

## 反爬虫

## CrawlSpider

## 分布式爬虫

# 爬虫伪装

## url的伪装

### 添加请求头

- 通过requests库添加header

## 请求频率

- 等待一会儿，使用`time.sleep`方法
