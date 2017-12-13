---
date: 2017-12-13
layout: post
title: "[JobHunt]leetcode - Largest Rectangle in Histogram "
categories: code
tags: leetcode
---

https://leetcode.com/problems/largest-rectangle-in-histogram/description/   
最简单的方法是O(N^2)两两组合扫一遍 但此题显然不是要考察这个   
可以maintain一个升序的stack   
只要遇到比stack top更大的元素 直接加入stack   
若遇到比stack top更小的元素 有意思的地方就来了:   

<!--more-->

> 设想`heights` = [1,2,4,5,3]   
> 当`stack`是[1,2,4,5] 然后遇到3的时候   
> 我们并不知道3会成为多大的矩阵的上限 所以我们每次只比较top位   
> 3比5(stack top位)小 那么必定可以组成一个3x2的矩阵   
> 3继续比4(新的stack top位)小 那么必定可以组成一个3x3的矩阵   
> 直到3比2(新的stack top位)大 又可以继续往后看 并且stack依然是一个升序序列   

但是我们如何保证heights一定在最后有一个小元素可以触发这个else branch呢?   
那么就是手动在heights后面加一个0   

代码如下   

{% highlight python %}
    def largestRectangleArea(self, heights):
        """
        :type heights: List[int]
        :rtype: int
        """
        if not heights:
            return 0
        heights.append(0)
        l = []
        size = 0
        i = 0
        n = len(heights)
        
        while i < n:
            if len(l) == 0 or heights[l[-1]] <= heights[i]:
                l.append(i)
                i += 1
            else:
                top = l.pop()
                height = heights[top]
                width = i if len(l) == 0 else i-l[-1]-1
                size = max(size, height*width)
        return size
{% endhighlight %}
