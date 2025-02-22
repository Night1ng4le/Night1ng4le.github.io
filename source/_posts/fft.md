---
title: 快速傅立叶变换（Fast Fourier Transform）
categories: [Advanced]
tags: [Algorithm]
mathjax: true
---

## 0x0 准备知识
&emsp;&emsp;其实是因为我自己完全没印象相关的知识了，所以这部分我就没有跳过。

### 0x01多项式
&emsp;&emsp;简单来说，形如 $$a_0+a_1X+a_2X^2+\cdots+a_nX^n$$ 的代数表达式叫做**多项式**，可以记作 $$P(X)=a_0+a_1X+a_2X^2+\cdots+a_nX^n$$ ， $$a_0,a_1,\cdots,a_n$$ 叫做**多项式的系数**，$$X$$是一个不定元，不表示任何值，不定元在多项式中`最大项`的次数称作多项式的次数。

<!--more-->

#### 多项式的系数表示法
&emsp;&emsp;像刚刚我们提到的那些多项式，都是以系数形式表示的，也就是将 $$n$$ 次多项式 $$A(x)$$ 的系数 $$a_0,a_1,\cdots,a_n$$ 看作 $$n+1$$ 维向量 $$\vec{a}=(a_0,a_1,\cdots,a_n)$$，其**系数表示**（coefficient representation）就是向量 $$\vec{a}$$ 。

#### 多项式的点值表示法
&emsp;&emsp;如果选取 $$n+1$$ 个不同的数 $$x_0,x_1,\cdots,x_n$$ 对多项式进行求值，得到 $$A(x_0),\cdots,A(x_n)$$ ，那么就称 $$\left( x_i,A\left( x_i \right)\right) : 0\leq i\leq n$$ 为多项式 $$A(x)$$ 的**点值表示**（point-value representation）。
&emsp;&emsp;多项式 $$A(x)$$ 的点值表示不止一种，你只要选取不同的数就可以得到不同的点值表示，但是任何一种点值表示都能唯一确定一个多项式，为了从点值表示转换成系数表示，可以直接通过**插值**的方法。

### 0x02复数

&emsp;&emsp;$$i=\sqrt{-1}$$

#### 复数的乘法
规定复数的乘法按照以下的法则进行：
设$$z_1=a+bi，z_2=c+di\left(a、b、c、d \in R\right)$$是任意两个复数，那么它们的积$$\left(a+bi\right)\left(c+di\right)=\left(ac-bd\right)+\left(bc+ad\right)i$$。
其实就是把两个复数相乘，类似两个多项式相乘，展开得: $$ac+adi+bci+bdi^2$$，因为$$i^2=-1$$，所以结果是$$\left(ac－bd\right)+\left(bc+ad\right)i$$ 。两个复数的积仍然是一个复数。
在极坐标下，复数可用模长$$r$$与幅角$$\theta$$表示为$$\left(r,\theta\right)$$。对于复数 $$a+bi$$，$$r=\sqrt{\left(a^2+b^2\right)}$$，$$\theta=arctan(\frac{b}{a})$$ 。此时，复数相乘表现为幅角相加，模长相乘。

#### 单位根
&emsp;&emsp;$$n$$ 次单位根是指能够满足方程 $$z^n=1$$ 的复数，这些复数一共有 $$n$$ 个它们都分布在复平面的单位圆上，并且构成一个正 $$n$$ 边形，它们把单位圆等分成 $$n$$ 个部分。
&emsp;&emsp;根据复数乘法相当于模长相乘，幅角相加就可以知道，$$n$$ 次单位根的模长一定是 $$1$$ ，幅角的 $$n$$ 倍是 $$0$$。



<未完待续...>










