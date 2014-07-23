---
layout: post
title: "C语言的缩进和空白"
date: 2013-12-02 21:31
comments: true
categories: [Linux, c]
---

C语言的缩进和空白使用原则
<!--more-->
<h1>一般编码缩进规则</h1>
<h2>1.字if、while、for与其后的控制表达式的(括号之间插入一个空格分隔，但括号内的表达式应紧贴括号</h2>
例如
<code> while (1) </code>
<h2>2.双目运算符的两侧各插入一个空格分隔，单目运算符和操作数之间不加空格</h2>
例如：
<code>i␣=␣i␣+␣1、++i、!(i␣<␣1)、-x、&a[1]等)</code>

<h2>3.后缀运算符和操作数之间也不加空格</h2>
例如:
取结构体成员<code>s.a</code>、函数调用<code>foo(arg1)</code>、取数组成员<code>a[i]</code>

<h2>4. ,号和;号之后要加空格，这是英文的书写习惯</h2>
例如：
<code>for␣(i␣=␣1;␣i␣<␣10;␣i++)、foo(arg1,␣arg2)</code>

<h2>5. 有时候为了突出优先级也可以写得更紧凑一些</h2>
例如：
<code>for␣(i=1;␣i<10;␣i++)</code>、<code>distance␣=␣sqrt(x*x␣+␣y*y)</code>等。但是省略的空格一定不要误导了读代码的人，例如<code>a||b␣&&␣c</code>很容易让人理解成错误的优先级.

<h2>6. 接近或大于80个字符的较长语句要折行写</h2>
由于UNIX系统标准的字符终端是24行80列的，接近或大于80个字符的较长语句要折行写，折行后用空格和上面的表达式或参数对齐，例如：
{% codeblock %}
if␣(sqrt(x*x␣+␣y*y)␣>␣5.0
    &&␣x␣<␣0.0
    &&␣y␣>␣0.0)
{% endcodeblock %}

再比如：
{% codeblock %}
foo(sqrt(x*x␣+␣y*y),
    a[i-1]␣+␣b[i-1]␣+␣c[i-1])
{% endcodeblock %}

<h2>7. 较长的字符串可以断成多个字符串然后分行书写</h2>
例如:
{%codeblock%}
printf("This is such a long sentence that "
       "it cannot be held within a line\n");
{%endcodeblock%}
C编译器会自动把相邻的多个字符串接在一起，以上两个字符串相当于一个字符串"This is such a long sentence that it cannot be held within a line\n"。

<h2>8. 在变量定义语句中用Tab字符，使变量名对齐</h2>
有的人喜欢在变量定义语句中用Tab字符，使变量名对齐，这样看起来很美观。

<h1>内核编码缩进规则</h1>

<h2>1.要用缩进体现出语句块的层次关系</h2>
要用缩进体现出语句块的层次关系，使用Tab字符缩进，不能用空格代替Tab。在标准的字符终端上一个Tab看起来是8个空格的宽度，如果你的文本编辑器可以设置Tab的显示宽度是几个空格，建议也设成8，这样大的缩进使代码看起来非常清晰。如果有的行用空格做缩进，有的行用Tab做缩进，甚至空格和Tab混用，那么一旦改变了文本编辑器的Tab显示宽度就会看起来非常混乱，所以内核代码风格规定只能用Tab做缩进，不能用空格代替Tab。

<h2>2. 语句块的{或}应该和关键字写在同一行，用空格隔开，而不是单独占一行</h2>
if/else、while、do/while、for、switch这些可以带语句块的语句，语句块的{或}应该和关键字写在同一行，用空格隔开，而不是单独占一行。例如应该这样写：
{%codeblock%}
if␣(...)␣{
       →语句列表
}␣else␣if␣(...)␣{
       →语句列表
}
{%endcodeblock%}

但很多人习惯这样写：
{%codeblock%}
if␣(...)
{
    →语句列表
}
else␣if␣(...)
{
    →语句列表
}
{%endcodeblock%}
内核的写法和[K&R]一致，好处是不必占太多行，使得一屏能显示更多代码。这两种写法用得都很广泛，只要在同一个项目中能保持统一就可以了。

<h2>3. 函数定义的{和}单独占一行，这一点和语句块的规定不同</h2>

{%codeblock%}
int␣foo(int␣a,␣int␣b)
{
    →语句列表
}
{%endcodeblock%}

<h2>4. switch和语句块里的case、default对齐写</h2>
switch和语句块里的case、default对齐写，也就是说语句块里的case、default标号相对于switch不往里缩进，但标号下的语句要往里缩进。例如：
{%codeblock%}
→switch␣(c)␣{
→case 'A':
→       →语句列表
→case 'B':
→       →语句列表
→default:
→       →语句列表
→}
{%endcodeblock%}

用于goto语句的自定义标号应该顶头写不缩进，而不管标号下的语句缩进到第几层。

<h2>5. 代码中每个逻辑段落之间应该用一个空行分隔开</h2>
例如每个函数定义之间应该插入一个空行，头文件、全局变量定义和函数定义之间也应该插入空行，例如：
{%codeblock%}
#include <stdio.h>
#include <stdlib.h>

int g;
double h;

int foo(void)
{
    →语句列表
}

int bar(int a)
{
    →语句列表
}

int main(void)
{
    →语句列表
}
{%endcodeblock%}

<h2>6. 一个函数的语句列表如果很长，也可以根据相关性分成若干组，用空行分隔。</h2>
一个函数的语句列表如果很长，也可以根据相关性分成若干组，用空行分隔。这条规定不是严格要求，通常把变量定义组成一组，后面加空行，return语句之前加空行，例如：

{%codeblock%}
int main(void)
{
    →int    →a, b;
    →double →c;

    →语句组1

    →语句组2

     →return 0;
}
{%endcodeblock%}

