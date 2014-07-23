---
layout: post
title: "递归与分治策略之整数划分"
date: 2013-09-18 10:49
comments: true
categories: [c++, algorithm] 
---
  将正整数划分为一些列正整数之和。在正整数n的所有不同的划分中，将最大加数n1不大于m的划分个数记为q(n, m).可以建立q(n, m)的递归关系。
<!--more-->
  1. q(n,1) = 1, n>=1
  2. q(n,m) = q(n,n) m>=n
  3. q(n,n) = 1+q(n,n-1)
  4. q(n,m) = q(n, n-1)+q(n-m, m), n>m>1：正整数n的最大加数不大于m的划分可以分成最大加数为m的划分和最大加数小于等于m-1的划分。

有递归关系可以写出递归函数。
{% codeblock lang:cpp %}
int q(int n, int m)
{
    if(n<1||m<1)    return 0;
    if(n==1||m==1)  return 1;
    if(n<m)         return q(n, n);
    if(n==m)        return 1+q(n, n-1);
    return q(n, m-1)+q(n-m, m);
}
{% endcodeblock %}

