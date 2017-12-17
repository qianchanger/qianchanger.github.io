---
date: 2017-12-17
layout: post
title: "[JobHunt]leetcode - Course Schedule III "
categories: code
tags: leetcode
---

https://leetcode.com/problems/course-schedule-iii/description/   
和course schedule I & II 完全无关的一道贪心题   
很类似于背包问题: 先把元素都排序一遍 然后尽量往包里捡    
如果捡不进去就把包头的吐出来比较一下 把较小的放在包里   
<!--more-->
为什么不需要比较包里面第二/第三/第四位呢? 因为元素已经排序过 如果比第一个大(而导致放不进去)    
那么就会因为比第二/第三/第四大(而放不进去了) 所以没必要比较   
最后包的长度 就是能够上的课的数量   

{% highlight python %}
    def scheduleCourse(self, courses):
        """
        :type courses: List[List[int]]
        :rtype: int
        """
        courses.sort(key=lambda x: x[1])
        import heapq
        heap = []
        
        duration = 0  # record the current usage of time alreay
        for course in courses:
            t, d = course
            if t + duration <= d:
                heapq.heappush(heap, (-t, t))  # the negative because heapq maintains a min-heap
                duration += t
            else:
                if heap[0][1] > t:
                    popout_item = heapq.heappop(heap)
                    heapq.heappush(heap, (-t, t))
                    duration = duration - popout_item[1] + t
        return len(heap)
{% endhighlight %}

----
Python标准库heapq太蠢了 居然没有max-heap的选项 必须用(-t, t)来存进去

----
第一次在机场刷题... XD