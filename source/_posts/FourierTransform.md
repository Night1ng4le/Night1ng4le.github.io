---
title: 傅立叶变换
categories: [Advanced]
tags: [Algorithm]
mathjax: true
---

**核心：从时域到频域的变换，这种变换是通过一组特殊的正交基来实现的。**

### 时域到频域
#### 时域
&emsp;&emsp;时域是描述一个数学函数或物理信号对时间的关系，这是生活中最容易感受的一种域。
&emsp;&emsp;很多物理量的定义都是基于时间产生的效果或者变化，以时间为参考会更容易理解，但更容易理解不意味方便使用。

<!--more-->

> 举个🌰～
> 一段音频波形图
![alt](https://pic4.zhimg.com/80/v2-3c724b7aa719464bfd5dc3ac4968cb3a_1440w.jpg?source=1940ef5c)
> 需求1：音量大一些
> 方案：让整体振幅增大（振幅=声音强度）
> 需求2: 加强低音部分
> 方案：无法单纯的加强低音


#### 频域
&emsp;&emsp;频域是描述频率所用到的空间或者说坐标系。频率是物质美妙完成周期性变化的次数。
&emsp;&emsp;对于前面提到的低音效果，可以简化为一个**低通滤波器**
![alt](https://pic4.zhimg.com/80/v2-36dbf0297d9d1c75bff7291a2c321e21_1440w.jpg?source=1940ef5c)
&emsp;&emsp;上图是低通滤波器的响应曲线，横轴是频率（Hz），纵轴是声音大小（dB）。所谓的低音效果，就是对声音中低音的部分保留或增强，对应上图中左侧的横线部分；而对于人声中的高音部分进行衰减，对应上图右侧斜坡的部分。通过这个简易的低通滤波器，我们就能将低音过滤，将高音衰减。
&emsp;&emsp;因此，低音效果是在频率范围内考虑问题，而波形图是在时域内的图像，所以如果想在时域内解决低音效果的问题，就像对牛弹琴。**所以我们要找到一个沟通时域和频域的桥梁，能够让时域和频域无障碍沟通。但，时域和频域表达的又只能是同一种信息，只是表现形式不同。**

### 时域转频域
#### 傅立叶级数
&emsp;&emsp;首先看一下标准正弦函数，时域中的方程为 $$y=sin \left( x \right)$$ ，图像如下
![alt](https://pic4.zhimg.com/50/v2-04985711b48fc218b5d6101e5f6cf4cc_hd.webp?source=1940ef5c)
&emsp;&emsp;而它的频率 $$f = \frac{1}{T} = \frac{1}{2\pi}$$ 。所以，上面这个函数在频域中的图像如下
![alt](https://pic4.zhimg.com/80/v2-8baab69933bff60fc4a5bc80cf05345c_1440w.jpg?source=1940ef5c)
&emsp;&emsp;更一般的有 $$y=Asin\left( 2\pi fx+\phi\right)$$ ，其中$$f$$是正弦函数频率，$$\phi$$是初始相位，$$A$$是幅度。在广义的频率中，$$f$$可正可负，上图中旋转臂顺时针旋转，$$f$$为负值。旋转臂状的越快，则频率越高，零时刻旋转臂和水平方向的夹角，就是初始相位。
&emsp;&emsp;由于正弦函数是单一频率，在频域中只需要一根竖线就能表现出来。我们期望的也是将时域的信号转换成一个个单一频率的正弦函数的组合，这样我们就能够在频域中用一根根竖线表示出来，也就完成了从时域到频域的转换。而上面提到的正弦函数表达式可以转换成 
$$y=Asin \left( 2\pi fx+ \theta \right)cos \left( 2\pi fx \right)+Acos \left( \theta\right) sin \left( 2\pi fx\right)=a_ncos \left( 2\pi fx \right)+b_nsin \left( 2\pi fx\right)$$


<未完待续...>
























