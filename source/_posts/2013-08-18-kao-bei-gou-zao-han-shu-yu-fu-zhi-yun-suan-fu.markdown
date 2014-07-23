---
layout: post
title: "拷贝构造函数与赋值运算符"
date: 2013-08-18 06:55
comments: true
categories: c++ 
---

总结一下：拷贝构造函数会逐一复制成员，所以如果对象里有指针，那么默认拷贝构造函数只会复制指针的内容，而不会为新对象分配相应的动态空间（存储指针所指向的内容），这样导致了两个对象的数据成员指向同一个地址，在释放空间时，导致同一块空间被释放两次这样的错误。同样赋值也会逐一复制成员，有指针成员也会导致析构这样释放空间的操作时出现错误，所以一般需要重写拷贝构造函数的类，也需要重写“=”赋值运算符。
<!--more-->

<h2>When do I need to write a copy constructor?</h2>
First, you should understand that if you do not declare a copy constructor, the compiler gives you one implicitly. The implicit copy constructor does a member-wise copy of the source object.
For example, given the class:

{% codeblock %}
  class MyClass {
      int x;
      char c;
      std::string s;
  };

{% endcodeblock %}

the compiler-provided copy constructor is exactly equivalent to:
{% codeblock %}
  MyClass::MyClass( const MyClass& other ) :
     x( other.x ), c( other.c ), s( other.s )
  {}
{% endcodeblock %}
In many cases, this is sufficient. However, there are certain circumstances where the member-wise copy version is not good enough. By far, the most common reason the default copy constructor is not sufficient is because the object contains raw pointers and you need to take a "deep" copy of the pointer. That is, you don't want to copy the pointer itself; rather you want to copy what the pointer
points to. Why do you need to take "deep" copies? This is typically because the instance owns the pointer; that is, the instance is responsible for calling delete on the pointer at some point (probably the destructor). If two objects end up calling delete on the same non-NULL pointer, heap corruption results.

Rarely you will come across a class that does not contain raw pointers yet the default copy constructor is not sufficient. An example of this is when you have a reference-counted object.
boost::shared_ptr<> is example.


<h2>When do I need to write an assignment operator?</h2>
First, you should understand that if you do not declare an assignment operator, the compiler gives you one implicitly. The implicit assignment operator does member-wise assignment of each data member from the source object. For example, using the class above, the compiler-provided assignment operator isexactly equivalent to:

{% codeblock %}
  MyClass& MyClass::operator=( const MyClass& rhs ) {
      x = other.x;
      c = other.c;
      s = other.s;
      return *this;
  }

{% endcodeblock %}
In general, any time you need to write your own custom copy constructor, you also need to write a custom assignment operator.
{% include_code  03copy_constructor_assignment.cpp %}
