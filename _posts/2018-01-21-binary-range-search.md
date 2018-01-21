---
date: 2018-01-21
layout: post
title: "[JobHunt]leetcode - Search for a Range "
categories: code
tags: leetcode
---

https://leetcode.com/problems/search-for-a-range/description/   

binary range search真的是我最最最讨厌的一类题   
边界条件总是很费心思去推算 & 验证   

<!--more-->

{% highlight python %}
def searchRange(self, nums, target):
    """
    :type nums: List[int]
    :type target: int
    :rtype: List[int]
    """
    if target not in nums:
        return [-1, -1]
    
    # find the lower bound
    le = 0
    ri = len(nums) - 1
    while le < ri:
        mid = (le + ri) / 2
        if nums[mid] >= target:
            ri = mid
        else:
            le = mid + 1
    
    lower_bound = le
    
    # find the upper bound 
    le = 0
    ri = len(nums) - 1
    while le < ri:
        mid = (le + ri) / 2 + 1
        if nums[mid] > target:
            ri = mid - 1
        else:
            le = mid
    
    upper_bound = le
    
    return [lower_bound, upper_bound]
{% endhighlight %}