---
layout: post
title: Deep learning notes
date: 2018-06-10 
categories: [deep learning]
tags: [deep learning]
---
Deep learning notes
<!--more-->

# part II - Deep Network: Modern Practices
## Chapter6 - Deep Feedforward Networks
### 6.2 Gradient-Based Learning
For feedforward neural networks, it is important to initialize all weights to small random values. The biases may be initialized to zero or to small positive values.
#### 6.2.1 Cost Function
In most cases, our patametric model defines a distribution $p(y|x;\theta)$ and we simply use the principle of maximum likelihood. This mean we use the cross-entropy between the training data and the model's predictions as the cost function.  
Mean squared error and mean absolute error often lead to poor results when used with gradient-based optimization. Some output units that saturate produce very small gradients when combined with these cost functions.
#### 6.2.2 Output Units
In general, if we define a conditional distribution $p(y|x;\theta)$, the principle of maximum likelihood suggests we use $-logp(y|x;\theta)$.  
It has been reported that gradient-based optimization of conditional Gaussian mixtures can be unreliable, in part because one gets divisions which can be numberically unstable. One solution is to clip gradients, while another is to scale the gradients heuristically.
### 6.3 Hidden Units
Unless indicated otherwise, most hidden units can be described as accepting a vector of inputs $x$, computing an affine transformation $z=W^Tx+b$, and then applying an element-wise nonlinear function $g(z)$. Most hidden units are distinguished from each other only by the choice of the form of the activation function $g(z)$.
#### 6.3.1 Rectified linear units and their generalizations
Rectified linear units are typically used on top of an affine transformation:
$$h=g(W^T+b).$$
When initializing the parameters of the affine transformation, it can be a good practice to set all element of $b$ to a small positive value, such as 0.1.  
One drawback to rectified linear units is that they canot learn via gradient-based methods on examples for which their activation is zero. Various generalizations of rectified linear units guarantee that they receive gradient everywhere.  
Three generalizations of rectified linear units are based on using a nonzero slope $\alpha_i$ when $z_i<0:h_i=g(z,\alpha)_i=max(0,z_i)+\alpha_imin(0,z_i)$. Absolute value rectification fixes $\alpha_i=-1$ to obtain $g(z)=|z|$. A leaky ReLU fixes $\alpha_i$ to a small value like 0.01, while a parametric ReLU, or PReLU, treats $\alpha_i$ as a learnable parameter.  
Maxout units generalize rectified linear units further. Each maxout unit then outputs the maximum element of one of these groups:
$$g(z)_i=\operatorname*{max}_{j\in G^{(i)}}z_j.$$
Where $G^{(i)}$ is the set of indices into the inputs for group $i,\{(i-1)k+1,...,ik\}$.  
Rectified linear units and all these generalizations of them are based on the principle that models are easier to optimize if their behavior is closer to linear. This same general priciple of using linear behavior to obtain easier optimization also applied in other contexts besides deep linear networks.
### 6.4 Architecture Design
#### 6.4.1 Universal approximation properties and depth
Specifically, the universal approximation theorem states that a feedforward network with a linear output layer and at leas one hidden layer with any "squashing" activation function can approximate any Borel measurable function from one finite-dimensional space to another with any desired nonzero amount of error, provide that the network is given enough hidden units. 
#### 6.4.2 Other architectural considerations
![Eﬀect of number of parameters.](/assets/2018-06-10/6-1.png)
