---
layout: post
title: "把cs50.h添加到库中"
date: 2013-10-11 23:25
comments: true
categories: [c, Linux, CentOS] 
---
  我最近在看网易公开课CS50，自我感觉非常喜欢David J. Malan的教学方法，非常羡慕和感慨哈佛学生的大学学习环境。也感谢网易为广大中国学生带来的福利。

  以下是自己网上搜素总结的如何模仿搭建CS50中Malan使用的开发环境。

  <!--more-->
1. 参考<a href="https://manual.cs50.net/library/"> CS50 Manual</a>，选择适合自己的安装方法
我的是Centos，所以执行以下命令，安装cs50库
    {% codeblock %}
      yum -y install gcc
      wget http://mirror.cs50.net/library50/c/library50-c-5.zip
      unzip library50-c-5.zip
      rm -f library50-c-5.zip
      cd library50-c-5
      gcc -c -ggdb -std=c99 cs50.c -o cs50.o
      ar rcs libcs50.a cs50.o
      chmod 0644 cs50.h libcs50.a
      mkdir -p /usr/local/include
      chmod 0755 /usr/local/include
      mv -f cs50.h /usr/local/include
      mkdir -p /usr/local/lib
      chmod 0755 /usr/local/lib
      mv -f libcs50.a /usr/local/lib
      rm -rf library50-c-5
    {% endcodeblock %}
  2. 安装完cs50库后, 修改make选项
    修改~/.bashrc文件
    在文件末尾添加
   {% codeblock %}
    # configure gcc
    export CC=gcc
    export CFLAGS="-ggdb -std=c99 -Wall -Werror -Wformat=0"
    export LANG=C
    export LDLIBS="-lcs50 -lm"
    alias gcc="gcc $CFLAGS"
    {% endcodeblock %}
  3. 执行source ~/.bashrc使更改后的bashrc文件生效
