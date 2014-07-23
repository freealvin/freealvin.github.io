---
layout: post
title: "Windows下Python安装模块"
date: 2013-08-27 17:39
comments: true
categories: python 
---
<!--more-->

以安装Beautifulsoup4为例：

1.到网站上下载：http://www.crummy.com/software/BeautifulSoup/bs4/download/

2.解压文件到C:\Python27

3.cmd运行C:\Python27\BeautifulSoup>python setup.py install

4.注意库名：creating build\lib\bs4

5.测试一下是否能导入：

>>> import bs4

如果不能导入，会提示：ImportError: No module named bs4
