---
date: 2014-11-13
layout: post
title: "[JobHunt]leetcode - Roman to Integer "
categories: code
tags: leetcode
---

Given a roman numeral, convert it to an integer.

<!--more-->
{% highlight python %}
def romanToInt(self, s):
    table = {
        'I': 1,
        'V': 5,
        'X': 10,
        'L': 50,
        'C': 100,
        'D': 500,
        'M': 1000
    }

    ret = 0

    for i in xrange(len(s)):
       if ((i>0) and (table[s[i]]>table[s[i-1]])):
            ret += table[s[i]] - 2 * table[s[i-1]]
        else:
            ret += table[s[i]]

    return ret
{% endhighlight %}
