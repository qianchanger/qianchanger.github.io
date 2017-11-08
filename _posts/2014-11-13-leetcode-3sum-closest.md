---
date: 2014-11-13
layout: post
title: "[JobHunt]leetcode - 3Sum Closest "
categories: code
tags: leetcode
---

>Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

<!--more-->
{% highlight cpp %}
int threeSumClosest(vector<int> &num, int target) {
    int diff = INT_MAX;
    int ret = 0;
    sort(num.begin(), num.end());
    for (int i=0; i<num.size()-2; i++) {
        int l = i+1;
        int r = num.size()-1;
        while (l<r) {
            int sum = num[i] + num[l] + num[r];
            int v = abs(sum-target);
            if (v < diff) {
                diff = v;
                ret = sum;
            }
            if (sum>target) {
                r--;
            } else {
                l++;
            }
        }
    }
    return ret;
}
{% endhighlight %}
