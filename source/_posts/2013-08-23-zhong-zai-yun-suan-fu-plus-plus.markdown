---
layout: post
title: "重载运算符++"
date: 2013-08-23 13:19
comments: true
categories: c++ 
---

自定义重载运算符++时，为了区分前++和后++，在重载后++时添加哑参数。
<!--more-->
{% codeblock lang:c++ %}
	F& operator++(){
		return *this;
	}
	F operator++(int){//此处使用到哑元
		F old(*this);
		return old;
	}
{% endcodeblock %}

由上可知，自定义重载的++运算符，前++往往比后++效率高，所以一般选择使用前++
