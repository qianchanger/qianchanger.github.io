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

### 找下届 - 找到target出现的第一次

> 我们希望把mid尽量往左靠 (因为是一个sorted array) --> (le + ri) / 2会往左靠   
> 如果nums[mid]大于target: 那么上界就是mid (显然)   
> 如果nums[mid]等于target: 那么上界依然是mid 因为我们希望把mid包含进来 因为mid本身可能是我们要找的第一次出现的target   
> 如果nums[mid]小于target: 那么下届一定是mid + 1 因为第一次出现的target必定不在mid 所以从mid + 1再开始找   
> 直到while loop条件破坏 (破坏的条件一定是le == ri, 因为步进一定是1, 不会出现上界小于下届的情况)   
> 此时任取le或者ri赋值给lower_bound   

### 找下届 - 找到target出现的最后一次 (即下一个元素一定比target大)

> 不同于找下届 找上界的时候我们希望把mid往大的方向上去靠 所以mid = (le + ri) / 2 + 1 , 这个加一就是往右靠一位   
> 如果nums[mid]大于target, 则mid一定不是我们要找的, 所以上界设为mid - 1   
> 如果nums[mid]等于target, 则mid可能是我们要找的最后一位target, 所以下届设为mid   
> 如果nums[mid]小于target, 则下届为mid 显然   
> 直到while loop停止, 同理, 此时le一定等于ri   
> 任意取le或者ri赋值给upper_bound   

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