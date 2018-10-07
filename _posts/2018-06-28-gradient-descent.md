---
layout: post
title: 机器学习梯度下降
date: 2018-06-29
categories:
- 机器学习
tags:
- 机器学习
---
机器学习梯度下降
<!--more-->

```python
import numpy as np
import matplotlib.pyplot as plt
```


```python
x_data = [338., 333., 328, 207., 226., 25., 179., 60., 208., 606.]
y_data = [640., 633., 619., 393., 428., 27., 193., 66., 226., 1591.]
```


```python
x = np.arange(-200, -100, 1) #bias
y = np.arange(-5, 5, 0.1) #weight
Z = np.zeros((len(x), len(y)))
X, Y = np.meshgrid(x, y)
for i in range(len(x)):
    for j in range(len(y)):
        b = x[i]
        w = y[j]
        Z[j][i] = 0
        for n in range(len(x_data)):
            Z[j][i] = Z[j][i] + (y_data[n] - b - w * x_data[n]) ** 2
        Z[j][i] = Z[j][i] / len(x_data)
```


```python
# ydata = b + w * xdata
b = -120 #initial b
w = -4 #initial w
lr = 1 # learning rate
iteration = 100000
# store initial values for plotting
b_history = [b]
w_history = [w]

# Adagrad 算法调节学习率
lr_b = 0
lr_w = 0

# iterations
for i in range(iteration):
    b_grad = 0.0
    w_grad = 0.0
    for n in range(len(x_data)):
        b_grad = b_grad - 2.0 * (y_data[n] - b - w * x_data[n]) * 1.0
        w_grad = w_grad - 2.0 * (y_data[n] - b - w * x_data[n]) * x_data[n]
    lr_b = lr_b + b_grad ** 2
    lr_w = lr_w + w_grad ** 2
    
    
    b = b - lr / np.sqrt(lr_b) * b_grad
    w = w - lr / np.sqrt(lr_w) * w_grad
    # store parameters for plotting
    b_history.append(b)
    w_history.append(w)
# plot the figure
plt.contourf(x, y, Z, 50, alpha=0.5, cmap=plt.get_cmap("jet"))
plt.plot([-188.4], [2.67], "x", ms=12, markeredgewidth=3, color="orange")
plt.plot(b_history, w_history, "o-", ms=3, lw=1.5, color="black")
plt.xlim(-200, -100)
plt.ylim(-5, 5)
plt.xlabel(r'$b$', fontsize=16)
plt.ylabel(r'$w$', fontsize=16)
#plt.show()
```




    <matplotlib.text.Text at 0x252cfda7e10>



# Gradient Descent
定义损失函数$L(\theta)$，$\theta$表示参数集合，$\theta=\{\theta_1,\theta_2,...,\theta_n\}$。
初始化$\theta为\theta^0，\theta^0=[\theta_1^0, \theta_2^0,...,\theta_n^0]$。
$\nabla L(\theta)=[\partial L(\theta_1)/\partial \theta_1, \partial L(\theta_2)/\partial \theta_2,..., \partial L(\theta_n)/\partial \theta_n]$
$$\theta^1 = \theta^0-\eta\nabla L(\theta^0)$$
$$\theta^k = \theta^{k-1}-\eta\nabla L(\theta^{k-1})$$

# Adagrad
$$\eta^t = \frac{\eta}{\sqrt{t+1}}$$
$$\sigma^t = \sqrt\frac{\sum_{i=0}^{t-1}(\nabla L(\theta^i))^2}{t+1}$$
$$\theta^t = \theta^{t-1}-\frac{\eta^{k-1}}{\sigma^{t-1}} \nabla L(\theta^{t-1})$$
$$\theta^t = \theta^{t-1}-\frac{\eta}{\sqrt{\sum_{i=0}^{t-1}(\nabla L(\theta^i))^2}} \nabla L(\theta^{t-1})$$

# 随机梯度下降
选取一个样本做损失函数

# Feature Scaling
$n$个样本，$m$个特征,数据 x
第$j$个特征的均值，$m_j=\frac{\sum_{i=1}^n  x_{ij}}{n}$  
第$j$个特征的标准差，$\sigma_j=\sqrt{\frac{\sum_{i=1}^n (x_{ij}-m_j)^2}{n-1}}$  
$$x_{ij}^{*}=\frac{x_{ij}-m_j}{\sigma_j}$$
那么经过特征缩放后每个特征的均值为0，方差为1


```python

```
