---
title: "快速傅里叶变化FFT"
date: 2023-04-10T16:24:18+08:00
draft: false
tags: [MATLAB]
categories: [学习生活]
featured_image: 
description: "快速傅里叶变化"

---



#  快速傅里叶变化（FFT）

[快速傅里叶变换FFT——有史以来最巧妙的算法](https://www.bilibili.com/video/BV1za411F76U/?spm_id_from=333.337.search-card.all.click&vd_source=a76b8a2a6d9a18738abcb916b7836085)

[这个算法改变了世界](https://www.bilibili.com/video/BV1CY411R7bA/?spm_id_from=333.1007.top_right_bar_window_history.content.click)

## 多项式乘法

n阶段多项式，使用n+1点表示



如何把系数表示转化为值表示，以及反过来将值表示转换成系数

## 把系数表示转化为值

想计算多项式P在n个点上的值，这n个点是一对对相反数
$$
P(x) = c0 + c1*x^1 + c2*x^2 + c3*x^3 + c4*x^4 + c5*x^5
$$

$$
P(x) = Pe(x^2) + x*Po(x^2)
$$

$$
Pe(x^2) = c4*x^4 + c2*x^2 + c0 \\
Po(x^2) = c5*x^4 + c3*x^2 + c1
$$



递归求两个小多项式，利用公式带回
$$
P(x_i) = Pe(x_i^2)+x_i*Po(x_i^2) \\
P(-x_i) = Pe(x_i^2)-x_i*Po(x_i^2)
$$



要求每个点都是对称的
$$
Points[\pm x_1,\pm x_2,\pm x_3,\pm x_4,...] is \pm paired \\
Points[x_1^2,x_2^2,x_3^2,x_4^2,...] not\pm paired
$$



进一步将每个数值对都实现对称

![image-20230409161902353.png](https://s2.loli.net/2023/04/09/JaRocMQvnhAgx1K.png)
$$
e^{i\theta} = cos(\theta) + isin(\theta)
$$
向量表示

![image-20230409162055262.png](https://s2.loli.net/2023/04/09/blXJQVYUs5ayNqt.png)
$$
P(w^j) = Pe(w^{2j})+w^jPo(w^{2j}) \\
P(w^{j+n/2}) = Pe(w^{2j}) - w^jPo(w^{2j})
$$
 写成程序

```python
def FFT(P):
n = len(P) # n is power of 2
if n == 1;
	return P
w = e^(2*pi*i/n)
Pe,Po = [p0,p2,...,pn-2],[p1,p3,...,pn-1]
ye,yo = FFP(Pe),FFT(Po)
y = [0]*n
for j in range(n/2):
    y[j] = ye[j] + wj*yo[j]
    y[j+n/2] = ye[j]-wj*yo[j]
return y
```

## 把值转化为系数表示

<img src="https://s2.loli.net/2023/04/12/zVPe3yFk1ArqL8x.png" alt="image-20230409164330499.png" style="zoom:50%;" />

<img src="https://s2.loli.net/2023/04/12/M1vIXC6OB9cU5eo.png" alt="image-20230409164346061.png" style="zoom:50%;" />

 

<img src="https://s2.loli.net/2023/04/12/y2jxDdKELk5r1Pi.png" alt="image-20230409164535095.png" style="zoom: 67%;" />

写成程序

```python
def FFT(P):
n = len(P) # n is power of 2
if n == 1;
	return P
w = (1/n)*e^(-2*pi*i/n)
Pe,Po = P[::2],P[1::2]
ye,yo = FFP(Pe),FFT(Po)
y = [0]*n
for j in range(n/2):
    y[j] = ye[j] + wj*yo[j]
    y[j+n/2] = ye[j]-wj*yo[j]
return y
```

## 总结

1. 将多项式用对应点值表示
2. 使用1的n次单位复根，每次平方完，还是正负成对出现
3. 单位复根特性，将点映射到复平面，对应复数坐标系
4. 反向插值基本一样，可以使用ffp方法解决ifft问题

### 傅里叶变换

将一个特定频率单位余弦信号与被测信号相乘，积分面积表示傅里叶信号幅值，单位正弦信号与被测信号相乘表示傅里叶信号相位



 