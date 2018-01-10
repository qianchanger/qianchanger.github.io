---
date: 2018-01-10
layout: post
title: "[JobHunt]leetcode - Palindrome Partitioning "
categories: code
tags: leetcode
---

https://leetcode.com/problems/palindrome-partitioning/description/   

这种要all possible result的题目 一般都可以用recursion   
在call recursion的前后 用append/pop来自己管理一下当前partial path   

<!--more-->

{% highlight python %}
class Solution(object):
    
    palindrome_cache = {}
    
    def partition(self, s):
        path = []
        result = []
        self.get_set(s, path, result)
        return result
        
    def get_set(self, s, path, result):
        import copy
        if s == '':
            result.append(copy.copy(path))
            return

        for i in range(1, len(s) + 1):
            if self.is_palindrome(s[:i]):
                path.append(s[:i])
                self.get_set(s[i:], path, result)
                path.pop()

    def is_palindrome(self, s):
        if s in self.palindrome_cache:
            return self.palindrome_cache[s]
        
        l = 0
        r = len(s) - 1
        while (l <= r):
            if s[l] != s[r]:
                self.palindrome_cache[s] = False
                return False
            l += 1
            r -= 1
            
        self.palindrome_cache[s] = True
        return True
{% endhighlight %}