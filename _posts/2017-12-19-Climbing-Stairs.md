---
date: 2017-12-19
layout: post
title: "[JobHunt]leetcode - Climbing Stairs "
categories: code
tags: leetcode
---

https://leetcode.com/problems/climbing-stairs/description/   
最近出差倒时差很累..刷点简单的题保持一下习惯就是了...
这题是简单的斐波那契数列 没有什么好多说的

<!--more-->

{% highlight python %}
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n <= 1:
            return 1
        
        dp = [0 for i in range(n + 1)]
        
        dp[0] = 1
        dp[1] = 1
        
        index = 2
        while index < len(dp):
            dp[index] = dp[index-2] + dp[index-1]
            index += 1
        return dp[-1]
{% endhighlight %}