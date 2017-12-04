---
date: 2017-12-04
layout: post
title: "[JobHunt]leetcode - Merge [Two/Multiple] Link List "
categories: code
tags: leetcode
---

https://leetcode.com/problems/merge-two-sorted-lists/description/   
https://leetcode.com/problems/merge-k-sorted-lists/description/   

思路非常的直观 也是链表操作的经典例题    
主要的一个trick就是造一个dummy-head    

<!--more-->

{% highlight python %}
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        fake_head = ListNode(None)
        cur_pos = fake_head
        
        while l1 is not None and l2 is not None:
            if l1.val <= l2.val:
                cur_pos.next = l1
                l1 = l1.next
            else:
                cur_pos.next = l2
                l2 = l2.next
            cur_pos = cur_pos.next
                
        if l1:
            cur_pos.next = l1
            
        if l2:
            cur_pos.next = l2
            
        return fake_head.next
{% endhighlight %}

第二题不能简单的每次比较N个链表的头再决定下一个node选谁   
这样导致我们需要O(N^2*K)的复杂度(K是每个链表长度)  
我们可以把链表按照val排序 这样复杂度可以降到O(NlgN*K)   
因为每次插入是lgN 总共需要操作N*K次

在Python中 可以自己写一个PriorityQueue 也可以调用标准库里面的PriorityQueue   

{% highlight python %}
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """  
        import Queue
        q = Queue.PriorityQueue()
        
        fake_head = ListNode(None)
        cur_pos = fake_head

        for l in lists:
            if l:
                q.put((l.val, l))
        
        while not q.empty():
            node = q.get()[1]
            cur_pos.next = node
            if node.next:
                q.put((node.next.val, node.next))
            cur_pos = cur_pos.next

        return fake_head.next
{% endhighlight %}