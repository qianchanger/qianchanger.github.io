---
date: 2017-12-09
layout: post
title: "[JobHunt]leetcode - Trapping Rain Water "
categories: code
tags: leetcode
---

## I
https://leetcode.com/problems/trapping-rain-water/description/   

最naive的思维: 找到底点 朝左右延伸到极限 然后计算面积就行了   

<!--more-->

{% highlight python %}
    # THIS SOLUTION CAN NOT PASS LTE
    def trap(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        def expand(index, height):
            le = index
            ri = index
            max_val_le = 0
            max_val_ri = 0
            while le - 1 >= 0 and height[le - 1] >= height[le]:
                le -= 1
                max_val_le = height[le - 1]
            while ri + 1 < len(height) and height[ri + 1] >= height[ri]:
                ri += 1
                max_val_ri = height[ri + 1]
            return le, ri, min(max_val_le, max_val_ri)
    
        i = 1
        size = 0
        while i < len(height):
            le, ri, cur_max_height = expand(i, height)
            if le == i or ri == i:
                continue
            for j in range(le, ri + 1):
                size += cur_max_height - height[j]
            i = re + 1
        return size
{% endhighlight %}

但是显这个思路显然过不了TLE   

Discussion tab提供了一个很骚的思路:   
想象右边有一个无限高的墙 那么从左往右扫一遍 能够装的水就是左边的极限   
再想象左边有一个无限高的墙 从右往左扫一遍 能够装的水就是右边的极限   
然后左右两边的极限的较小值 就是真实的能够装的水量   

{% highlight python %}
    def trap(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        height_le = []
        max_le = 0        
        for i in range(len(height)):
            max_le = max(max_le, height[i])
            height_le.append(max_le)

        height_ri = []
        max_ri = 0
        for i in range(len(height))[::-1]:
            max_ri = max(max_ri, height[i])
            height_ri.append(max_ri)
        height_ri = height_ri[::-1]
            
        size = 0
        for i in range(len(height)):
            size += (min(height_le[i], height_ri[i]) - height[i])
        return size
{% endhighlight %}

## II
一个很tricky的思路:   
一个容器可以装多少水取决于最短的边有多高 那么就把border放进一个heap里   
然后从heap top(最短边)出发   
开始往内延伸 用一个visited_map来记录已经计算过的点   
一个inner点的height值应该是它自己的值和延伸到它的点的值的较大值   

{% highlight cpp %}
    def trapRainWater(self, heightMap):
        """
        :type heightMap: List[List[int]]
        :rtype: int
        """
        if not heightMap:
            return 0
        
        m = len(heightMap)
        n = len(heightMap[0])
        
        visited_map = [[0 for j in range(n)] for i in range(m)]        
        
        import heapq
        heap = []
        for i in range(m):
            for j in range(n):
                if i in (0, m-1) or j in (0, n-1):
                    heap.append((heightMap[i][j], (i, j)))
                    visited_map[i][j] = 1
        heapq.heapify(heap)
        
        volume = 0
        while heap:
            height, (i, j) = heapq.heappop(heap)
            for x, y in [(i+1, j), (i-1, j), (i, j+1), (i, j-1)]:
                if 0 <= x < m and 0 <= y < n and not visited_map[x][y]:
                    volume += max(0, height - heightMap[x][y])
                    heapq.heappush(heap, (max(height, heightMap[x][y]), (x, y)))
                    visited_map[x][y] = 1
        return volume
{% endhighlight %}

