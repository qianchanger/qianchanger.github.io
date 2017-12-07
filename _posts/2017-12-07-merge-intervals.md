---
date: 2017-12-06
layout: post
title: "[JobHunt]leetcode - Merge/Insert Intervals "
categories: code
tags: leetcode
---

https://leetcode.com/problems/merge-intervals/description/   
https://leetcode.com/problems/insert-interval/description/   

也算是一种经典面试题类型 也有一个trick 就是上来直接按照interval.start来排序   
这样merge的时候 就只需要看前后两位   
如果前后两位不能merge 那么第三位`势必`不能merge   
<!--more-->

因为我们是按照interval.start来排序的   
如果1.end < 2.start, 那么一定1.end < 3.start (2.start < 3.start)   
基于这个特性 我们用x, y (初始化为0, 1) 从左到右把List扫一遍就行了   
时间复杂度是O(N)

{% highlight python %}
    def merge(self, intervals):
        """
        :type intervals: List[Interval]
        :rtype: List[Interval]
        """
        if len(intervals) < 2:
            return intervals
        
        intervals = sorted(intervals, key=lambda x: x.start)
        x = 0
        y = 1
        while y < len(intervals):
            if intervals[x].end >= intervals[y].start:
                intervals[x] = Interval(intervals[x].start, max(intervals[x].end, intervals[y].end))
                intervals.pop(y)
            else:
                x += 1
                y += 1
        return intervals
{% endhighlight %}

## Insert Intervals   
我猜想应该是想要考察Quick Select, 用O(lgN)的复杂度把新加入的interval给merge进去   
但somehow直接把第一问的答案复制到第二问 也可以accepted 复杂度是O(N)   
估计是给Python的时间冗余太多了吧...   

{% highlight python %}
    def insert(self, intervals, newInterval):
        """
        :type intervals: List[Interval]
        :type newInterval: Interval
        :rtype: List[Interval]
        """
        # COPY FROM 56 START
        def merge(intervals):
            """
            :type intervals: List[Interval]
            :rtype: List[Interval]
            """
            if len(intervals) < 2:
                return intervals

            intervals = sorted(intervals, key=lambda x: x.start)
            x = 0
            y = 1
            while y < len(intervals):
                if intervals[x].end >= intervals[y].start:
                    intervals[x] = Interval(intervals[x].start, max(intervals[x].end, intervals[y].end))
                    intervals.pop(y)
                else:
                    x += 1
                    y += 1
            return intervals
        # COPY FROM 56 END
        
        intervals.append(newInterval)
        return merge(intervals)
{% endhighlight %}


