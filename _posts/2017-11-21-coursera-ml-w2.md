---
layout: post
title: "Coursera ML - W2 - Linear Regression"
tags: coursera
---

时隔4年 对于这门经典课程的内容已经淡忘 于是又复习一遍 在这里记下一些感受和领悟

# Cost function 
\\(J(\theta) = \frac{1}{m}\sum_{i=1}^m(h_\theta(X^i) - Y^i) \\)
其目的是找到一个theta的向量 去最小化\\(J(\theta)\\)

怎么找到这个theta的向量呢? 有两个方法
其一是normal equation 这是数学的方法
第二是gradient descent 这是ML的方法

# Normal Equation
线性回归的方程 \\(h_\theta(X) = \theta^T * X \\) 导致了它的导数在每一个维度一定是凹函数
那么总体来看 我们一定可以通过数学运算找到一个所有维度上都最小的\\(\theta\\)组合来满足\\(J(\theta)\\)最小
只要提供的m个数据是互不相关 且\\(m > n\\) 那么通过数学运算就一定可以求得\\(\theta\\)

但是此方法的缺点在于 矩阵运算求逆的复杂度是\\(O(n^3)\\) 如果n很大 那么就完全算不完

# Gradient Descent
同理 如果线性回归的\\(J(\theta)\\)是convex函数的话 那么通过不断递进的调整\\(\theta\\)我们一样可以得到最优解
且这个最求解就是global optimal.

# 一般多项式
通过对于feature的处理 可以使用linear regression来表示一般多项式 只要feature之间是相加的关系