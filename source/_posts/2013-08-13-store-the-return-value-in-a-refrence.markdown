---
layout: post
title: "Store the Return Value In a Refrence"
date: 2013-08-13 06:57
comments: true
categories: c++ 
---
  C++中，临时对象生存周期和它被创建时整个语句的生命长度相同，但是我们可以将临时变量赋值给const reference来延长它的生命长度。
<!--more-->

  我在学习C++中的运算符重载时没有注意到这一点，导致编译失败。我的代码是这样写的：
{% codeblock %}
class Fraction{
	int n;
	int d;
	……

	public:
		……
		Fraction operator+( const Fraction &f2)const;
		friend istream &operator>>(istream &in, Fraction &f);
		friend ostream &operator<<(ostream &out,Fraction &f);
};

Fraction Fraction::operator+( const Fraction &f2)const
{
	Fraction res(n*f2.d + d*f2.n, d*f2.d);
	return res;
}

//重载>>，以便于输入
istream &operator>>(istream &in , Fraction &f)
{
	char c;
	in>> f.n >> c >> f.d;
	return in;
}
//重载<<，便于输出
ostream &operator<<(ostream &out, Fraction &f)// non-const reference
{
	out<< f.n << '/' << f.d;
	return out;
}

int main()
{
	Fraction f1;
	Fraction f2;
	cin>>f1>>f2;
	cout<<f1+f2<<endl;//temp f1+f2, operator<<(cout, temp), it's not allowed to bind the temporary value to a non-const reference
	return 0;
}
{% endcodeblock %}

  在测试重载<<运算符时，输出定义的对象cout<<f1， 没有问题，但当我试着输出cout<<f1+f2时，编译出现了错误
{% codeblock %}
 error: no match for ‘operator<<’ in ‘std::cout << operator+(((Fraction&)(& f1)), ((Fraction&)(& f2)))’
 note:                 std::ostream& operator<<(std::ostream&, Fraction&)
{% endcodeblock %}
后来查询了资料后，发现是重载<<运算符时，形参的类型导致的。形参f的类型是Fraction &， 而我调用cout<<f1+f2时， f1+f2会调用 f1.operator+(f2)并返回一个临时结果，而错误就出现在这个临时结果上，临时结果是不能改变的，而重载<<时参数的是Fraction &，而不是const Fraction &，而在C++中是不允许把temporary绑定到non-const reference上的，所以编译器会出现以上的错误。


这个练习的所有代码:
{% include_code 03operator_overload.cpp %}
