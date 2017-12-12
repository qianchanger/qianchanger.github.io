---
date: 2017-12-11
layout: post
title: "[JobHunt]leetcode - Russian Doll Envelopes "
categories: code
tags: leetcode
---

https://leetcode.com/problems/russian-doll-envelopes/description/   

这题有个很直观的O(N^2)的DP解法   
但是python过不了LTE   

<!--more-->
{% highlight python %}
    def maxEnvelopes(self, envelopes):
        """
        :type envelopes: List[List[int]]
        :rtype: int
        """
        if not envelopes:
            return 0
        
        envelopes = sorted(envelopes)
        n = len(envelopes)
        dp = [1 for x in range(n)]
        
        for i in range(n):
            for j in range(i):
                if envelopes[j][0] < envelopes[i][0] and envelopes[j][1] < envelopes[i][1]:
                    dp[i] = max(dp[i], dp[j] + 1)
        return max(dp)
{% endhighlight %}

参考了discussion tab 发现可以转化成LIS来做   
思路骚到没朋友:   
> 把envelope按照第一个元素排升序 第一个元素相同时按照第二个元素排降序   
> 直接取第二个元素组成的list来找longest increasing subsequence   

{% highlight python %}
    def maxEnvelopes(self, envelopes):
        """
        :type envelopes: List[List[int]]
        :rtype: int
        """
        if not envelopes:
            return 0
        
        import bisect
        envelopes = sorted(envelopes, key=lambda x: (x[0], -x[1]))
        
        lis = []
        for i in map(lambda x: x[1], envelopes):
            pos = bisect.bisect_left(lis, i)
            if pos == len(lis):
                lis.append(i)
            else:
                # no need for min() here because we already desc sorted for 2nd value in L11
                lis[pos] = i
        return len(lis)
{% endhighlight %}

----
明天要复习一下LIS这个问题   