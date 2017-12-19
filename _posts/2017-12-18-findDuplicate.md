---
date: 2017-12-18
layout: post
title: "[JobHunt]leetcode - Find the Duplicate Number "
categories: code
tags: leetcode
---

https://leetcode.com/problems/find-the-duplicate-number/description/   
总共n+1个数 数值在1到n之间 其中某一个(或多个有重复) (显然有重复 因为数值只能在1到n之间但是有n+1个数)   
这题有很多限制条件 比如空间O(1) 时间O(N^2)   
但总体来说 有一种很直观的思路:   
初始下限是1 初始上限是n 中间值是mid   
如果比mid小的数比mid的值多 那么说明重复发生在mid以下 重置上限为mid   
反之 如果比mid小的数比mid的值小或者一样多 说明重复发生在mid以上 重置下限为mid + 1   

<!--more-->

思路很直观 代码如下

{% highlight python %}
    def findDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        low = 1
        high = len(nums) - 1
        
        while low < high:
            mid = low + (high - low) / 2
            
            count = 0
            for i in nums:
                if i <= mid:
                    count += 1
                    
            if count <= mid:
                low = mid + 1
            else:
                high = mid
        return low
{% endhighlight %}

----
## 第二种思路 
看到discussion板块有人说这题可以像链表追逐找重合点一样   
一想还真是 思路如下:   
n+1长度的数组 每一位里面存的值 代表了指向序号为值的另一节点   
(e.g. [3,1,2] 第一位3指向第三位2 第三位2指向第二位1 第二位1指向第一位3)   
两个追逐指针就可以解决这个问题   
有一个很好的post在http://keithschwarz.com/interesting/code/?dir=find-duplicate   