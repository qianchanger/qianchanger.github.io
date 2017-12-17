---
date: 2017-12-16
layout: post
title: "[JobHunt]leetcode - Course Schedule I & II "
categories: code
tags: leetcode
---

## I
https://leetcode.com/problems/course-schedule/description/   
非常简单基础的图遍历问题 一个小trick就是在每个Node记录入度(`指入它的边的数量`)   
入度为零 折加入queue还是遍历   
如果所有的prerequisites都可以被我们遍历一遍 那么就说明prerequisites是满足条件的   

<!--more-->

{% highlight python %}
class Node(object):

    def __init__(self, val):
        self.val = val
        self.children = set()
        self.incoming_edge_count = 0
        
    def add_child(self, val):
        self.children.add(val)

            
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        node_dict = {}
        for pair in prerequisites:
            b, a = pair

            if a not in node_dict:
                node_dict[a] = Node(a)
            
            if b not in node_dict:
                node_dict[b] = Node(b)
                
            node_dict[a].add_child(b)
            node_dict[b].incoming_edge_count += 1        
            
        q = list()
        for i, node in node_dict.items():
            if node.incoming_edge_count == 0:
                q.append(node)
        
        while q:
            node = q.pop(0)
            children = node.children
            for child in children:
                node_dict[child].incoming_edge_count -= 1
                if node_dict[child].incoming_edge_count == 0:
                    q.append(node_dict[child])
            del node_dict[node.val]
        
        return True if not node_dict else False
{% endhighlight %}

## II
https://leetcode.com/problems/course-schedule-ii/description/   
基本可以重用题目I的代码 只是加入一个chain来记录走过的Node就行了   

{% highlight python %}
class Node(object):

    def __init__(self, val):
        self.val = val
        self.children = set()
        self.incoming_edge_count = 0
        
    def add_child(self, val):
        self.children.add(val)

class Solution(object):
    def findOrder(self, numCourses, prerequisites):
        node_dict = {}
        
        for pair in prerequisites:
            b, a = pair

            if a not in node_dict:
                node_dict[a] = Node(a)
            
            if b not in node_dict:
                node_dict[b] = Node(b)
                
            node_dict[a].add_child(b)
            node_dict[b].incoming_edge_count += 1        
            
        q = list()
        for i, node in node_dict.items():
            if node.incoming_edge_count == 0:
                q.append(node)
        
        # first, take the courses that are not in any prerequisites pairs
        all_courses = set([i for i in range(numCourses)])
        courses_with_dependancy = set(node_dict.keys())
        courses_without_dependancy = all_courses - courses_with_dependancy
        dependancy_chain = []
        dependancy_chain.extend(list(courses_without_dependancy))
            
        # now, deal with courses with dependancy
        while q:
            node = q.pop(0)
            children = node.children
            for child in children:
                node_dict[child].incoming_edge_count -= 1
                if node_dict[child].incoming_edge_count == 0:
                    q.append(node_dict[child])
            dependancy_chain.append(node.val)
            del node_dict[node.val]
        
        return dependancy_chain if not node_dict else []
{% endhighlight %}