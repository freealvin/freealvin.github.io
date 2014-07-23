---
layout: post
title: "Embed code with Include_code"
date: 2013-08-07 11:43
comments: true
categories: 
---
<!--more-->
Import files on your filesystem into any blog post as embedded code snippets with syntax highlighting and a download link. In the _config.yml you can set your code_dir but the default is source/downloads/code. Simply put a file anywhere under that directory and use the following tag to embed it in a post.
Syntax

{%include_code test.js%}


此行测试编码
'''C# Test
	System.Console.WriteLine("Hello World!");
'''
