---
date: 2017-12-06
layout: post
title: "[JobHunt]leetcode - Minimum Window Substring "
categories: code
tags: leetcode
---

https://leetcode.com/problems/minimum-window-substring/description/   

对于这一类题 也有很常规的trick:   
1. 用一个hashmap来记录已经读过了那些character   
2. 用头尾两个指针[位置]来表示substring的范围   

<!--more-->

程序大体上照这么一个思路来运行:   
0. 左边指针和右边指针都初始化为0 [都在s的最左端]   
1. 右边指针[right]开始往右走 直到满足某条件[在本题中 是满足了substring包含t的所有元素以及数量]   
2. 左边指针[left]也开始往右走 直到上一步中的条件又被破坏掉   
3. #1, #2重复执行 相当于左边指针一直在`追逐`右边指针 两个指针把s都扫描了一遍 所以复杂度是O(n)   

{% highlight python %}
    def minWindow(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: str
        """
        import collections
        record = collections.defaultdict(int)
        left = 0
        right = 0
        min_distance = float('inf')
        begin = None
        end = None
        
        for c in t:
            record[c] += 1
        
        while (right < len(s)):
            if s[right] in t:
                record[s[right]] -= 1
            right += 1
            
            while all([v <= 0 for v in record.values()]):
                if right - left < min_distance:
                    min_distance = right - left
                    begin = left
                    end = right
                if s[left] in t:
                    record[s[left]] += 1
                left += 1
        
        if begin is not None:
            return s[begin:end]
        return ""
{% endhighlight %}

在LeetCode的讨论版 有一个帖子对于substring的总结非常到位   
https://discuss.leetcode.com/topic/30941/here-is-a-10-line-template-that-can-solve-most-substring-problems/2   
也提供了一个模板 (抄过来 记录在下)

{% highlight cpp %}
int findSubstring(string s){
        vector<int> map(128,0);
        int counter; // check whether the substring is valid
        int begin=0, end=0; //two pointers, one point to tail and one  head
        int d; //the length of substring

        for() { /* initialize the hash map here */ }

        while(end<s.size()){

            if(map[s[end++]]-- ?){  /* modify counter here */ }

            while(/* counter condition */){ 
                 
                 /* update d here if finding minimum*/

                //increase begin to make it invalid/valid again
                
                if(map[s[begin++]]++ ?){ /*modify counter here*/ }
            }  

            /* update d here if finding maximum*/
        }
        return d;
  }
{% endhighlight %}
