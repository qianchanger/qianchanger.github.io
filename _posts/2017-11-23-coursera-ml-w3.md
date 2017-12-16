---
layout: post
title: "Coursera ML - W3 - Logistic Regression"
tags: coursera
---

# 为什么会有logistic regression

supervised learning做预测大体分为输出连续值的regression问题和输出离散变量的classification问题

上一周讨论了用线性回归来做regression 那么自然而然就会想到同样的方法可以不可以使用来做classification?

问题显而易见
1. linear regression的model \\(h_\theta(X) = \theta^T * X\\) 的范围是\\(-\infty, +\infty\\)内的实数; 而classification的Y是有限的离散变量  
2. \\(h_\theta(X) = \theta^T * X\\)中间的threshold难以划分 Y值的0.5处不一定准确  

<!--more-->

于是 为了修正以上的两点问题
我们引入了sigmoid函数 \\(g(z) = \frac{1}{1 + e^{-z}}\\)
此函数有一些很适合做classification的特性:
Predict True时, g(z) >= 0.5, z也>=0; vice versa.


# Logistic Regression cost function
使用传统的 \\(\frac{1}{2m}\sum_{i=1}^m(h_\theta(X) - Y)^2\\)不是不行, 就是将sigmoid方程带入并对\\(\theta\\)求偏微分之后的函数不是凹函数, 得不到global optimal.
所以我们构建了另外一个cost function
\\(-ylog(h_\theta(x) - (1-y)log(1-h_\theta(x)))\\)

这个方程有个好处, 预测值与实际值偏离越远, penalty越重. 并且偏微分也是凹函数.


# Gradient Descent
初始方程和linear regression一致 都是   
Repeat {  
    \\(\theta_j := \theta_j - \alpha\frac{\partial}{\partial\theta_j}J(\theta)\\)   
}  

因为初始方程一致 所以偏微分之后的方程也一样   
Repeat {  
    \\(\theta_j := \theta_j - \frac{\alpha}{m}\sum_i=1^m(h_\theta(X^i) - Y^i)X_j^i\\)   
}  

但值得注意的是 由于\\(h_\theta(X)\\)的定义不一样了 所以其实虽然形式上是一样的但内容已经变化了

# Multi-class classfication
这个问题很好处理 把一个大问题转化为很多个小问题就行了   
比如\\(Y\in{A, B, C}\\)   
那么就可以train三个模型 分别预测   
Y是不是A,   
Y是不是B,   
Y是不是C,   

# Solve the problem of overfitting
如果我们添加很多的多次元 那么很可能model就会被overfit   
如何来解决这个问题呢   
一是可以减少feature的数量 可以人工或者用机器来选择feature 但是这代表我们会损失一些信息 这样解决并不是特别完美   
二是可以引入regularization 就是在cost function中加入\\(\theta^2\\) 这样去惩罚过大的\\(\theta\\) 防止overfitting   
值得注意的是 我们不惩罚\\(\theta_0\\)   