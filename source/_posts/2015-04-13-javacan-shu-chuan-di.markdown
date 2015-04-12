---
layout: post
title: "java参数传递"
date: 2015-04-13 01:55:00 +0800
comments: true
categories: [java, 基础]
---

参数传递分为值传递和引用传递，Java是面向对象的编程语言，又是如何传递参数的呢？

<!--more-->

Java的值传递和其他语言的类似，没有什么特别的，这里主要介绍对象作为参数的传递。对象作为参数，传递的是对象的引用吗？其实不是。

先面给出一个例子
```java

public static void swap(Employee x, Employee y)
{
	Employee temp = x;
	x = y;
	y = temp;
}
```

如果Java对对象采用的是引用调用，那么这个方法就能实现交换数据的效果：

```java
	Employee a = new Employee("alvin");
	Employee b = new Employee("nathan");
	swap(a,b);
```
结果会是a变成nathan， b变成alvin吗？最终的结果并没有变化，a仍为alvin，b也仍为nathan。

这个过程说明，Java采用的不是引用调用。实际上，对象引用进行的是<bold>值传递</bold>。

下面总结一下：
	1. 方法不能修改一个基本数据类型的参数

	2. 方法可以改变对象参数的状态

	3. 方法不能对对象参数引用一个新对象。


