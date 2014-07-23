---
layout: post
title: "C++ operator overloading"
date: 2013-08-12 16:42
comments: true
categories: c++
---
In C++ the overloading principle applies not only to functions, but to operators too. That is, of operators can be extended to work not just with built-in types but also classes. A programmer can provide his or her own operator to a class by overloading the built-in operator to perform some specific computation when the operator is used on objects of that class. 

<!--more-->
<h2>An example of operator overloading</h2>

{% include_code 03operator_overload.cpp %}

In order to allow operations like cin>>f, in above code we overloaded the ">>"operator. And in order to access the private memebers in the implementations, we use keyworkd "friend".A important trick that can be seen in this general way of overloading IO is the returning reference for istream/ostream which is needed in order to use them in a recursive manner:

{% codeblock %}
cin>>f1>>f2;
{% endcodeblock %}
