---
date: 2018-01-28
layout: post
title: "[JobHunt]leetcode - Evaluate Division "
categories: code
tags: leetcode
---

https://leetcode.com/problems/evaluate-division/description/   

一开始有点懵 不明白这题要考察什么 (说明这个题出得很好 很迷惑人)   
开车的时候突然意识到 这是个graph traversal   
构建graph 然后DFS就可以得出答案   
不需要任何优化就可以AC   

<!--more-->

{% highlight python %}
class Solution(object):
    def calcEquation(self, equations, values, queries):
        """
        :type equations: List[List[str]]
        :type values: List[float]
        :type queries: List[List[str]]
        :rtype: List[float]
        """
        # construct graph
        import collections
        path = collections.defaultdict(list)
        path_weight = {}
        node_set = set()
        
        for p, weight in zip(equations, values):
            src, dst = p

            # forward edge
            path[src].append(dst)
            path_weight[(src, dst)] = weight

            # backward edge
            path[dst].append(src)
            path_weight[(dst, src)] = 1.0 / weight

            # self loop
            path_weight[(dst, dst)] = 1.0
            path_weight[(src, src)] = 1.0
            
            node_set.add(src)
            node_set.add(dst)
                
        ret = []

        for query in queries:
            src, dst = query
            
            import copy
            connect_set = copy.copy(node_set)
            connect_set.discard(src)
            
            val = self.calculate_connected_ndoes_weight(
                src,
                dst,
                path,
                path_weight,
                connect_set,
            )
            ret.append(val)
        
        return ret
            
    def calculate_connected_ndoes_weight(self, src, final_dst, path, path_weight, connect_set):
        if not connect_set:
            return -1

        if (src, final_dst) in path_weight:
            return path_weight[(src, final_dst)]
        
        for dst in path[src]:
            if dst in connect_set:
                connect_set.discard(dst)
                val = self.calculate_connected_ndoes_weight(dst, final_dst, path, path_weight, connect_set)
                connect_set.add(dst)
                if val != -1:
                    return path_weight[(src, dst)] * val
        return -1
{% endhighlight %}