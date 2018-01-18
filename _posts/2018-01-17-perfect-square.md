---
date: 2018-01-17
layout: post
title: "[JobHunt]leetcode - Perfect Squares "
categories: code
tags: leetcode
---

https://leetcode.com/problems/perfect-squares/description/   

有很多种思路可以做出来   
显而易见的有DP 复杂度是O(N^2)   
也可以BFS 把N想象成树根 每个node都有\\(\sqrt{N}\\)个子节点(不过只考虑不小于零)   
层层迭代 则可以算出层数 有零的层的层数 就是需要的平方数的个数   
复杂度麻...worst case是O(N^2) 所以没比DP慢   

<!--more-->

{% highlight python %}
def numSquares(n):
    """
    :type n: int
    :rtype: int
    """
    import copy
    # build a list of square numbers that are <= n
    elem_list = []
    i = 1
    while (i ** 2 <= n):
        elem_list.append(i ** 2)
        i += 1
        
    this_level = set()
    next_level = set()
    
    this_level.add(n)
    
    level_count = 0
    while this_level or next_level:
        for node in this_level:
            l = set([node - i for i in elem_list if node - i >= 0])
            if 0 in l:
                return level_count + 1
            next_level = next_level.union(l)
        this_level = copy.copy(next_level)
        next_level = set()
        level_count += 1
{% endhighlight %}