---
date: 2018-01-25
layout: post
title: "[JobHunt]leetcode - Queue Reconstruction by Height"
categories: code
tags: leetcode
---

https://leetcode.com/problems/queue-reconstruction-by-height/description/   

<!--more-->

这是一道很精巧的题目 我个人很喜欢   


> people先按照身高`降序`排列 若身高相同 则k值小的排前面 (可以忍受前面比自己高的人少的排前面)   
> 构建一个空ret list   
> 对于排序后的people中的 每一个元素来说   
> 已经在ret中的 一定大于等于自己 自己可以接受前面几人比自己高 就插入ret的第几位置     
> 而余下来 每个新元素只会比在ret中的元素 小或等于身高 所以新插入不会影响ret已有的排序   

{% highlight python %}
def reconstructQueue(self, people):
    people = sorted(people, key=lambda (h, k): (-h, k))
    ret = []
    for e in people:
        ret.insert(e[1], e)
    return ret
{%  endhighlight %}