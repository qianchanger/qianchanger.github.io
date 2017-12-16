---
layout: post
title: "Coursera ML - W5 - Neural Network"
tags: coursera
---

没有单独写W4的内容 因为Week 4仅仅是讲了Neural Network的模型表达   
所以和W5合写一份笔记   

# 为什么会有Neural Network?
在有了`Liner Regression`和`Logistic Regression`分别处理regression和classification这两类问题之后   
为什么我们还需要`Neural Network`呢?   
有一个很实际的原因: 在现实生活中 有一些classfication问题的feature很多很多   
那么使用`Logistic Regression`来计算大量feature的问题 是昂贵且慢的   

<!--more-->

比如说让机器识别一张50 x 50的RGB图 那么就是有7500个feature 一旦我们打算加上二次/三次/四次项   
那么`Logistic Regression`基本上是算不了的   

这个时候就需要Neural Network   
它本质上 是用原始feature去学习到了新feature   
层层迭代 最终得出预测值   

# Multi-class Neural Network
不像`Logistic Regression` 需要拆分成多个Model来解决multi-class   
对于NN来说 可以直接让Output layer输出多个值   

# 一些记号 - Forward Propagation
\\(a_i^j\\) = activation of Neuron i in layer j   
\\(\Theta^j\\) = matrix of weights mapping \\(layer_j\\) to \\(layer_{j+1}\\)   
\\(z^{l+1} = \Theta^l * a^l ; a^{l+1} = sigmoid(z^{l+1})\\)   
通过以上算式即可算出最终的output   

# Cost Function
回想`Logistic Regression`的cost function:   
\\(J(\theta) = -\frac{1}{m}\sum_{i=1}^m[-y^ilog(h_\theta(x^i)) - (1-y^i)log(1-h_\theta(x^i))] + \frac{\lambda}{2m}\sum_{j=1}^n\theta_j^2\\)   
`Logistic Regression`是单输出 但NN是K输出;    
`Logistic Regression`的\\(\theta\\)是一个vector 但NN的\\(\Theta\\)是L个matrix (L层)   
所以NN的cost function是一个更generalized的函数 (增加了K的维度和L维度):   
\\(J(\Theta) = -\frac{1}{m}\sum_{i=1}^m\sum_{k=1}^K[-y_k^ilog(h_\Theta(x^i)) - (1-y_k^i)log(1-h_\Theta(x^i))] + \frac{\lambda}{2m}\sum_{l=1}^{L-1}\sum_{i=1}^{S_l}\sum_{j=1}^{S_{l+1}}(\Theta_{j,i}^l)^2\\)   
注意\\(h_\Theta(x)\\)是指整个forward propagation   

# Backpropagation Algorithm
上面我们得到了Cost Function   
显然 如果我们想对每一个\\(\Theta_{j,i}^l\\)求导的话 整个计算量是巨大的   
并且这个Cost Function也并不是convex的    
那么有何种办法可以计算出每一个l,j,i对应的\\(\frac{\partial}{\partial(\Theta_{j,i}^{l})}J(\Theta)\\)呢?

> \\(\delta^l = a^l - y\\) (输出层)   
> \\(\delta^{l-1} = ((\Theta^l)^T\delta^{l}) .* g'(a^{l-1})\\) (其中g'()代表是sigmoid对a的导数)   
> \\(\delta^{l-1} = ((\Theta^l)^T\delta^{l}) .* a^{l-1} .* (1 -a^{l-1})\\) (将g'()取导之后带入上式)   
> 于是就有了 \\(\Delta^l = \Delta^l + \delta^{l+1}(a^l)^T\\)   
> 最终\\(D_{i,j}^l = \frac{1}{m}(\Delta_{i,j}^l + \lambda\Theta_{i,j}^l) , if j \ne 0\\)

上面迭代的原理我是完全没听懂的 但是最终我们可以通过数学验证的方式验证 这样求导出来的D的数值 确实是导数的值   
这一点在`Gradient Checking`这一步里面讲到了   

# Backpropagation Implementation details
为了让这个算法真正可以工作 我们还需要一些小工具   
1. unrolling matrix to vectors  
2. gradient checking - 验证backpropagation计算出来的数值是正确的   
3. random initialization - 因为如果\\(\Theta\\)都初始化为0的话 每一层的所有Neuron就完全一样了 (symmetry)   
4. 使用至少1+层hidden layer 并且每层hidden layer的Neurons数量一致 且越多越好   