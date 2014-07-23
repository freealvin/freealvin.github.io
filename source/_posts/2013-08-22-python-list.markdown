---
layout: post
title: "python list"
date: 2013-08-22 12:18
comments: true
categories: python 
---
list是python里非常强大的数据类型
<!--more-->
<h2>list 复制</h2>
{% codeblock %}
>>> l1=[1,2,3]
>>> l2=l1
>>> l1[0]=10
>>> print l1
[10, 2, 3]
>>> print l2
[10, 2, 3]
>>>
{% endcodeblock %}


<h2>如何复制？</h2>
{% codeblock %}
>>> l2=l1[:]
>>> print l2
[10, 2, 3]
>>> l1[0]=24
>>> print l1
[24, 2, 3]
>>> print l2
[10, 2, 3]
>>>
{% endcodeblock %}
发生了什么？ 第一种是**指向**，其实还是同一个内容。 第二种是**复制**。

<h2>本质上的区别</h2>

{% codeblock %}
>>> l2 = l1
>>> l2 == l1 #值相同
True
>>> l2 is l1 #指向同一个地方
True
>>> l2 = l1[:]
>>> l2 == l1 #值相同
True
>>> l2 is l1 #并不是指向同一个地方
False
{% endcodeblock %}


<h2>list如何添加元素？</h2>
{% codeblock %}
>>> l1=[]
>>> l1[0]="a"
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list assignment index out of range
{% endcodeblock %}
为什么？ 因为l1等于一个空列表，没有空间。 l1[0]是需要空间的。

我们该怎么让空list存储数据?

list有一写默认的函数

{% codeblock %}
l1.append("a")
{% endcodeblock %}

<h2>删除成员的方法</h2>

{% codeblock %}
>>> l1.append("b")
>>> l1.append("c")
>>> l1.append("d")
>>> l1.append("b")
>>> print l1
["b", "c", "d","b"]
>>> l1.remove("b")
>>> print l1
["c", "d","b"]
>>> l1.remove("b")
>>> print l1
["c","d"]
{% endcodeblock %}
还有

l1.pop()
再试一个删除的高级用法
{% codeblock %}
>>> print l1
[2, 3, 4, 5]
>>> del l1[1:3]
>>> print l1
[2, 5]
{% endcodeblock %}


<h2>如何插入一个元素：</h2>

{% codeblock %}
>>> l1.insert(1,67)
>>> print l1
[2, 67, 5]
{% endcodeblock %}

