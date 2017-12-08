---
date: 2017-12-08
layout: post
title: "[JobHunt]leetcode - Kth Smallest Element in a Sorted Matrix "
categories: code
tags: leetcode
---

https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/description/   

这是一道有Paper具体研究的题.. 最佳的复杂度是O(lgN) 大约是基于quick select的一个变种算法   
但是在面试的时候 显然是做不出来这种复杂度的code   
所以这里推荐一个O(KlgN)的做法   
堆的插入复杂度是O(lgN) 需要插入K次   

{% highlight python %}
    def kthSmallest(self, matrix, k):
        """
        :type matrix: List[List[int]]
        :type k: int
        :rtype: int
        """
        import heapq
        
        n = len(matrix)
        l = []
        
        for i in range(n):
            l.append((matrix[i][0], (i, 0)))
            
        heapq.heapify(l)
        value = None
        while k:
            k -= 1
            value, (x, y) = heapq.heappop(l)
            if y + 1 < n:
                 heapq.heappush(l, (matrix[x][y+1], (x, y+1)))
        return value
{% endhighlight %}