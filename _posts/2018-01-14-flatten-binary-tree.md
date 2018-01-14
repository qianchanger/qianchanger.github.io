---
date: 2018-01-14
layout: post
title: "[JobHunt]leetcode - Flatten Binary Tree to Linked List "
categories: code
tags: leetcode
---

https://leetcode.com/problems/flatten-binary-tree-to-linked-list/description/   

这个题目本身不复杂 对于每一个node 就是先整备node.left 于是node.left已经是一个flatten list之后   
把这个list赋到node.right(当然要把node.right暂时保存到tmp)   
然后找到node最右最右最右 把tmp接上去 继续整备tmp就行了   
代码如下    

<!--more-->

{% highlight python %}
def flatten(self, node):
    if not node:
        return
    
    self.flatten(node.left)
    
    tmp = node.right
    node.right, node.left = node.left, None
    
    cur = node
    while cur.right:
        cur = cur.right

    cur.right = tmp
    
    self.flatten(tmp)
{% endhighlight %}

## 优化
但是这段代码并不好 因为每次我们整备一个子树 需要traversal一次    
每次找最右节点 又要traversal一次 每个node就要访问两边   
在disucussion板块看到一个用prev 存下每次flatten的node作为prev   
这就非常有灵性了   

修改代码如下:

{% highlight python %}
prev = None
def flatten(self, node):
    if not node:
        return
    
    self.prev = node
    
    self.flatten(node.left)
    
    tmp = node.right
    node.right, node.left = node.left, None
    self.prev.right = tmp
    
    self.flatten(tmp)
{% endhighlight %}

当然复杂度依然是O(N) 不过每个node只需要traversal一次了