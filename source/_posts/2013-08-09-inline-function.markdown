---
layout: post
title: "inline function"
date: 2013-08-09 13:20
comments: true
categories: c++
---
<!--more-->  
c++中不提倡使用宏，如果是宏函数可以用inline函数替换，如果是宏常量，用const常数替换。
  inline是用于实现的关键字，也就是说定义内联函数时，inline关键字必须和函数定义体放在一起，在函数声明时使用不起任何作用

{% include_code inline.cpp %}
