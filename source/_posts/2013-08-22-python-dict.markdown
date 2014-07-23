---
layout: post
title: "python dict"
date: 2013-08-22 13:07
comments: true
categories: python 
---
#dict
字典的用法，dict的查找特别快捷。如果我们的项目经常用到搜索某些数据，最好用dict类型。
<!--more-->
<h2>创建dict</h2>
{% codeblock lang:python %}
dict1 = {}
{% endcodeblock %}

或者
{% codeblock lang:python %}
>>> dict(sape=4139, guido=4127, jack=4098)
{'sape': 4139, 'jack': 4098, 'guido': 4127}
{% endcodeblock %}

或者用dict构造函数创建dict变量
{% codeblock lang:python %}
dict2 = dict([(key1, value1),(key2,value2),...]
{% endcodeblock %}

表达式创建
{% codeblock lang:python %}
>>> dict3 = {x: x**2 for x in (2, 4, 6)}
{2: 4, 4: 16, 6: 36}
{% endcodeblock %}

<h2>添加元素</h2>

{% codeblock lang:python %}
tel = {}
#dict1[key] = value
tel['guido'] = 4127
tel['jack'] = 4098
tel['sape'] = 4193
{% endcodeblock %}


<h2>获取元素值</h2>
{% codeblock lang:python %}
num1 = tel['sape']
{% endcodeblock %}
如果键不存在，tel[key]操作会出错，所以在获取元素之前，需要判断元素键是否存在
判断方法？
{% codeblock lang:python %}
	if tel.get("snape"):
		num1 = tel["snape"]
{% endcodeblock %}

或者
{% codeblock lang:python %}
	if "snape" in tel:
		num1 = tel["snape"]
{% endcodeblock %}

<h2>删除元素</h2>
{% codeblock lang:python %}
del tel["guido"]
#tel.pop("jack")
{% endcodeblock %}


<h2>遍历</h2>
迭代器：
{% codeblock lang:python %}
>>> knights = {'gallahad': 'the pure', 'robin': 'the brave'}
>>> for k, v in knights.iteritems():
...     print k, v
...
gallahad the pure
robin the brave
{% endcodeblock %}




