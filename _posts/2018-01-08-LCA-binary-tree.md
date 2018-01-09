---
date: 2018-01-08
layout: post
title: "[JobHunt]leetcode - Lowest Common Ancestor of a Binary Tree "
categories: code
tags: leetcode
---

https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/description/   

如果有一个node 它的左非空 右非空 那么它自己就是LCA   
如果p是q的祖先(或者q是p的祖先) 那么一路上都是最后一行反馈回去 也可得到p(或q)   
非常简洁的recursive思路   

<!--more-->

{% highlight python %}
    def lowestCommonAncestor(self, root, p, q):
        if not root:
            return None
        
        if root == p or root == q:
            return root
        
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)
        
        if left and right:
            return root
        
        return left if left is not None else right
{% endhighlight %}

此题其他语言还可以把path找出来 直接比对   
但对于python来说 会LTE   
不过复习一下怎么把path找出来 也是不错的   

{% highlight python %}
class Solution(object):
    def lowestCommonAncestor(self, root, p, q):
        if p == root or q == root:
            return root

        path_to_p = []
        self.findpath(root, p, path_to_p)
        
        path_to_q = []
        self.findpath(root, q, path_to_q)

        i_p = len(path_to_p) - 1
        i_q = len(path_to_q) - 1
        while (i_p >= 0 and i_q >= 0):
            if path_to_p[i_p] == path_to_q[i_q]:
                i_p -= 1
                i_q -= 1
        
        if i_p >= 0:
            return path_to_p[i_p + 1]
        elif i_q >= 0:
            return path_to_q[i_q + 1]

    def findpath(self, root, node, path):
        if not root:
            return False

        path.append(root)
        if root == node:
            return True
        
        
        if (root.left != None and self.findpath(root.left, node, path)
            or root.right != None and self.findpath(root.right, node, path)):
            return True
        
        path.pop()
        return False
{% endhighlight %}