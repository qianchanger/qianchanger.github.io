---
date: 2018-01-09
layout: post
title: "[JobHunt]leetcode - Lowest Common Ancestor of a Binary Search Tree "
categories: code
tags: leetcode
---

https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/description/   

类似昨天的题目 不过由于是BST 所以代码更简单   

<!--more-->

{% highlight python %}
    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        if p.val > q.val:
            tmp = p
            p = q
            q = tmp

        if root.val >= p.val and root.val <= q.val:
            return root
        
        elif root.val > p.val:
            return self.lowestCommonAncestor(root.left, p, q)
        
        else:
            return self.lowestCommonAncestor(root.right, p, q)
{% endhighlight %}