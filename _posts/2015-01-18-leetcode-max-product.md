---
date: 2015-01-18
layout: post
title: "[JobHunt]leetcode - Maximum Product Subarray "
categories: code
tags: leetcode
---

题目连接点击:[这里](https://oj.leetcode.com/problems/maximum-product-subarray/)

<!--more-->
{% highlight cpp %}
int maxProduct(int A[], int n) {
    vector<int> array(n, 0);
    array[0] = A[0];
    for (int i = 1; i < n; ++i) {
        int val = 1;
        array[i] = A[i];
        for (int j = i; j >= 0; --j) {
            val *= array[j];
            array[i] = max(array[i], val);
        }
    }
    return array[n-1];
}
{% endhighlight %}
LTE

搜索后 得一O(n)算法
{% highlight cpp %}
int maxProduct(int A[], int n) {
    if (n <= 0) {
        return 0;
    }
    if (n == 1) {
        return A[0];
    }
    int max_local = A[0];
    int min_local = A[0];
    int global = A[0];
    for (int i = 1; i < n; ++i) {
        int max_local_bk = max_local;
        max_local = max(A[i], max(A[i] * max_local, A[i] * min_local));
        min_local = min(A[i], min(A[i] * max_local_bk, A[i] * min_local));
        global = max(global, max_local);
    }
    return global;
}
{% endhighlight %}

---
明日即将启程 飞赴洛杉矶 第一个onsite 加油
