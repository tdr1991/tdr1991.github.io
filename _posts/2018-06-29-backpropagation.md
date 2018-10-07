---
layout: post
title: 深度学习反向传播
date: 2018-06-29
categories:
- 深度学习
- 机器学习
tags:
- 深度学习
- 机器学习
---
深度学习反向传播
<!--more-->

# 反向传播算法（backpropagation）
此算法是一个有效计算梯度的方法，C表示损失函数，常见的是交叉熵
$$L(\theta)=\sum_{n=1}^N C^n(\theta)$$
$$\Longrightarrow  \frac{\partial L(\theta)}{\partial w}=\sum_{n=1}^N \frac{\partial C^n(\theta)}{\partial w}$$
假设 $z=x_1 w_1+x_2 w_2 +b$，激活函数为$\sigma$，那么$z$经过激活函数输出$a，a=\sigma (z)$  
那么 $$\frac{\partial C}{\partial w}=\frac{\partial C}{\partial z}\frac{\partial z}{\partial w}$$
正向计算：  
$$\frac{\partial z}{\partial w_1}=x_1$$
$$\frac{\partial z}{\partial w_2}=x_2$$
反向计算：
$$\frac{\partial a}{\partial z}=\sigma'(z)$$
假设第一层输出 $z'=a w_3+..., z''=a w_4+...$  
$$\frac{\partial C}{\partial z}=\frac{\partial C}{\partial a}\frac{\partial a}{\partial z}$$
$$\frac{\partial C}{\partial a}=\frac{\partial C}{\partial z'}\frac{\partial z'}{\partial a}+\frac{\partial C}{\partial z''}\frac{\partial z''}{\partial a}$$
$$\frac{\partial z'}{\partial a}=w_3, \frac{\partial z''}{\partial a}=w_4$$
$$\frac{\partial C}{\partial z}=\sigma'(z)[w_3 \frac{\partial C}{\partial z'}+w_4\frac{\partial C}{\partial z''}]$$
![](/assets/images/dl/bp.jpg)


```python

```
