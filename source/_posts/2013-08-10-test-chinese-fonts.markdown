---
layout: post
title: "Test Chinese Fonts"
date: 2013-08-10 20:58
comments: true
categories: [Linux, CentOS]
---

解决CentOS中文显示问题：
一：安装中文支持
{% codeblock %}
# yum install "@Chinese Support"
{% endcodeblock %}

二：安装字体
{% codeblock %}
# yum install fonts-chinese.noarch
{% endcodeblock %}

三：修改配置文件
{% codeblock%}
# vi /etc/sysconfig/i18n
{% endcodeblock %}
将
{% codeblock %}
LANG="en_US.UTF-8" 
SYSFONT="latarcyrheb-sun16" 
{% endcodeblock %}

修改为
{% codeblock %}
LANG="zh_CN.GB18030" 
LANGUAGE="zh_CN.GB18030:zh_CN.GB2312:zh_CN" 
SUPPORTED="zh_CN.UTF-8:zh_CN:zh:en_US.UTF-8:en_US:en" 
SYSFONT="lat0-sun16"
{% endcodeblock%}

四：
{% codeblock %}
# cd /usr/share/fonts/
# fc-cache   -fv
{% endcodeblock %}
