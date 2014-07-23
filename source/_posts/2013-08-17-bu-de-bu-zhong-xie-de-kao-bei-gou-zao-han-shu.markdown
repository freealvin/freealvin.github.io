---
layout: post
title: "不得不重写的拷贝构造函数"
date: 2013-08-17 19:39
comments: true
categories: c++ 
---
	自定义一个栈类，使用一个栈对象初始化另一个对象，自然会用到拷贝构造函数，代码如下
{% include_code copy_constructor.cpp %}
以上代码在执行的时候会出现：
{% codeblock %}
*** glibc detected *** ./a.out: double free or corruption (fasttop)
{% endcodeblock %}
也就是说，我们释放了两次动态分配的空间。为了解决这个问题，我们需要重写拷贝构造函数，在拷贝构造函数中重写申请新对象的动态空间。
{% codeblock %}
Stack(const Stack &t):mem(new T[t.max]), len(t.len), max(t.max){}
{% endcodeblock %}
