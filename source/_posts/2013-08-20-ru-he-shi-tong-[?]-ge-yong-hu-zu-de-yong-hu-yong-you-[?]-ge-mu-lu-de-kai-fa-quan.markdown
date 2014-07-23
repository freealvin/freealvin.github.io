---
layout: post
title: "如何使同一个用户组的用户拥有一个目录的开发权"
date: 2013-08-20 06:17
comments: true
categories: Linux 
---
<!--more-->
1.添加项目组
  {% codeblock %}   #groupadd poject{% endcodeblock %}
2.添加获得project支持的用户
{% codeblock %}
     #useradd -G project alex
     #useradd -G project arod
{% endcodeblock %}
3.创建目录
    {% codeblock %} #mkdir /srv/ahome{% endcodeblock %}
4.把目录的用户组改为project
    {% codeblock %} #chgrp project /srv/ahome {% endcodeblock %}
5.更改目录的权限，是project用户组可以rwx,其他人没有任何权限
  {%codeblock %}   #chmod 770 /srv/ahome{% endcodeblock %}

6.切换到alex,并在/srv/ahome下创建一个文件，查看文件的权限
     {% codeblock %}
     #su - alex
     $touch abcd
     $ll
{% endcodeblock %}
     会发现abcd 的拥有者、group均为alex,而arod虽然对文件夹有rwx权限，但对于刚刚创建的文件可以删除却不能编辑
7.这就要用到SGID
{% codeblock %}     $exit
     #chomd 2770 /srv/ahome
{% endcodeblock %}
     这样执行者在执行的过程中会自动获得该程序用户组的支持 
     

