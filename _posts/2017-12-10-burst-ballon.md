---
date: 2017-12-10
layout: post
title: "[JobHunt]leetcode - Burst Balloons "
categories: code
tags: leetcode
---

https://leetcode.com/problems/burst-balloons/description/   

典型的DP题: 一段i,j之间的最大值要计算i < k < j的所有组合   
所以用一个2D matrix存储计算过的i,j段   

<!--more-->

{% highlight python %}
    def maxCoins(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        nums = [1] + nums + [1]
        n = len(nums)
        dp = [[0 for x in range(n)] for x in range(n)]
        
        def find_maxium(i, j):
            if dp[i][j]:
                return dp[i][j]
            
            coins = 0
            for k in range(i+1, j):
                coins = max(coins, nums[i] * nums[k] * nums[j] + find_maxium(i, k) + find_maxium(k, j))
            dp[i][j] = coins
            return coins
        
        return find_maxium(0, n-1)
{% endhighlight %}