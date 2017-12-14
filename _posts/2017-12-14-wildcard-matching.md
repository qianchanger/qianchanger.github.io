---
date: 2017-12-14
layout: post
title: "[JobHunt]leetcode - Wildcard Matching "
categories: code
tags: leetcode
---

这是一道贪心算法的题 (当然也可以用DP做出来)   
为什么说是贪心算法呢?   
因为我们希望尽量`少`用p里面的*去match s里面的字符 而尽量去消耗p里面的其他字符   

<!--more-->

逻辑如下:   
> 如果p和s相同 或者p是?的话 都往后移   
> 如果p是* 那么只移动p 不移动s   
> 继续循环 如果发现s和p不match 但是之前又发现了一个*的话 那么就移动1位s 同时p保持为*的下一位   
> 继续循环 如果发现s和p还是不match 那么又继续移动1位s 重复#3和#4 这样`尽量`少用*去消耗s 而主动去消耗p   
> 直到外层循环结束 如果都还没有match的话 那么直接return False

代码如下:   
{% highlight python %}
    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        
        s_cur = p_cur = 0
        s_star_i = p_star_i = None
        
        while s_cur < len(s):
            if p_cur < len(p) and (s[s_cur] == p[p_cur] or p[p_cur] == '?'):
                s_cur += 1
                p_cur += 1
            elif p_cur < len(p) and p[p_cur] == '*':
                s_star_i = s_cur
                p_star_i = p_cur
                p_cur += 1  # only move p forward, we want to match as least * as possible.
            elif p_star_i is not None:
                # well, we have to use * to match some chars in s
                s_star_i += 1  # match a char in s
                s_cur = s_star_i
                p_cur = p_star_i + 1  # put p_cur to the char after * again, try to match more non-* chars.
            else:
                return False
            
        while p_cur < len(p) and p[p_cur] == '*':
            p_cur += 1
            
        return True if p_cur == len(p) else False
{% endhighlight %}
