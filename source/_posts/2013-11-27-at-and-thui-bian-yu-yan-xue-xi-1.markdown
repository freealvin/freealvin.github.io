---
layout: post
title: "AT&amp;T汇编语言学习1"
date: 2013-11-27 09:14
comments: true
categories: 
---
<!--more-->
<h1>一. AT&T汇编语法格式</h1>

(1) 寄存器引用
    引用寄存器要在寄存器号前加%，如move %eax, %ebx

(2) 操作数顺序
    操作数排列是从源（左）到目的（右）， 如
{% codeblock %}
move %eax, %ebx
# %eax为源, %ebx为目的地址
{% endcodeblock %}

(3) 常数/立即数的格式<br/>
    使用立即数，要在数前加$，如mov $4, %ebx 
    符号常数直接引用 如mov value, %ebx
    引用符号地址在符号前加$，如mov $value, %ebx

(4) 操作数的长度<br/>
    操作数的长度用加在指令后的符号表示
    b(byte)
    w(word)
    l(long)
    如：mov w%ax, %bx


<h1>二. 转移和调用</h1> 
(1) 在AT&T汇编格式中，绝对转移和调用指令(jmp/call)的操作数前 要加上'*'作为前缀<br/>
(2) 远转移指令和远调用指令的操作码，在AT&T汇编格式中为"ljump"和"lcall",在Itel汇编格式中则为"jmp far"和"call far"<br/>

AT&T格式

{% codeblock %}
ljump $section, $offset
lcall $section, $offset
{% endcodeblock %}
Intel格式
{% codeblock %}
jump far section:offset
call far section:offset
{% endcodeblock %}

(3) 远程返回指令<br/>
    
{% codeblock %}
lret $stack_adjust
ret far stack_adjust
{% endcodeblock %}

(4) 寻址方式<br/>
    用section:disp(base, index, scale)表示，计算方法是:
        base + index*scale + disp

    section:[base+index*scale+disp] #Intel
    
{% codeblock %}
movl -4(%ebp), %eax                    mov eax, [ebp-4]
movl array(, %eax, 4), %eax            mov eax, [eax*4+array]
movw array(%ebx, %eax, 4), %cx         mov cx, [ebx+4*eax+array]
movb $4, %fs:(%eax)                    mov fs:eax, 4
{% endcodeblock %}
