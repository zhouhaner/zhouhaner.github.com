---
author: Jim zhou
layout: post_full
title: Python learning
featimg: 2.jpg
tags: [python]
category: [standard]
---

京东买了本书，就是想搞好web，结果发现web是在太凶猛了。那天做实验，跟师兄说以后想做产品经理。师兄问我，产品经理是做什么的，实话，我并不清楚。

百度了一下解释，也就苏杰的解释很通俗易懂。（不会写md文档了，还翻阅了一下手册，发现功能有强大了）

>所谓产品经理：就是设计解决某个问题的东西的那个人

附带了一些我自我认识：产品经理，就得东许多东西，博古通今级别的。于是我开始了web学习。购买的是一本Flask Web开发，基于Python的一本书。
意味着什么呢，我在跟着书上敲着代码的时候，我发现我必须得学习Python了，哦，对了，还有数据库。

###一开始我是拒绝的，我做实验哪来那么多时间看啊。但想想还是觉得蛮有挑战的，接下，开始学吧。

Python是个很有趣的语言，蛇性！拓展性良好。

##变量类型
###变量赋值
变量赋值奇怪了，不需要定义。一段简单的代码就看懂了:
---python
#coding=utf-8
#!/usr/bin/python

counter = 100 # 赋值整型变量
miles = 1000.0 # 浮点型
name = "John" # 字符串

print counter
print miles
print name
---
哈哈，不需要**声明**
###标准数据类型
Python的标准数据类型包含5种：数字，字符串，列表，元组，字典（我看到字典的时候我是崩溃的，数据量好大）。

####python数字
Python支持四种不同的数值类型：
>* int（有符号整型）
>* long（长整型[也可以代表八进制和十六进制]）
>* float（浮点型）
>* complex（复数）

####Python字符串
（1）Python字符串，和所有字符串组成都是一样的，都是数字，字母，下划线。
（2）Python字符串有两种取值顺序：
>从左到右索引默认从0开始，最大范围是字符串长度少1
>从右到左索引默认从-1开始，最大范围是字符串的开头。

对字符串的操作是有趣的，再来一串代码，轻松看懂！
---python
#coding=utf-8
#!/usr/bin/python

str = 'Hello World!'

print str # 输出完整字符串
print str[0] # 输出字符串中的第一个字符
print str[2:5] # 输出字符串中第三个至第五个之间的字符串
print str[2:] # 输出从第三个字符开始的字符串
print str * 2 # 输出字符串两次
print str + "TEST" # 输出连接的字符串
---

基本所有语言都是helloworld开。。

####Python列表
Python列表和R、Matlab很相似。练操作都是相似的。使用量很多。
---python
#coding=utf-8
#!/usr/bin/python

list = [ 'abcd', 786 , 2.23, 'john', 70.2 ]
tinylist = [123, 'john']

print list # 输出完整列表
print list[0] # 输出列表的第一个元素
print list[1:3] # 输出第二个至第三个的元素 
print list[2:] # 输出从第三个开始至列表末尾的所有元素
print tinylist * 2 # 输出列表两次
print list + tinylist # 打印组合的列表
---

####Python元组
元组在Python所表示的也是数组，阿赫，就是和列表差了个[] ().但是有些操作也是不一样的，这里指的注意。
列表里的那一段代码，只需要将[]更改为（），就是元组操作了。这里就不列举代码了。一般使用的就是[]。

####Python元字典
字典字典，就是什么都有，说的学术一点，就是：字典是无序的对象的集合。地点当中的元素是通过键来存取的，相对比列表的偏移存取是不相同的。
---python
#coding=utf-8
#!/usr/bin/python

dict = {}
dict['one'] = "This is one"
dict[2] = "This is two"

tinydict = {'name': 'john','code':6734, 'dept': 'sales'}


print dict['one'] # 输出键为'one' 的值
print dict[2] # 输出键为 2 的值
print tinydict # 输出完整的字典
print tinydict.keys() # 输出所有键
print tinydict.values() # 输出所有值
---

今日开始学起走，明日继续！
