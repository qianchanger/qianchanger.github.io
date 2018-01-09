---
date: 2017-12-20
layout: post
title: "[JobHunt]leetcode - Convert Sorted Array to Binary Search Tree "
categories: code
tags: leetcode
---

https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/description/   


{% highlight python %}
    def _build_tree(self, nums, start, end):
        if start > end:
            return
        
        mid = (start + end) / 2
        ret = TreeNode(nums[mid])
        ret.left = self._build_tree(nums, start, mid - 1)
        ret.right = self._build_tree(nums, mid + 1, end)
        return ret

    def sortedArrayToBST(self, nums):
        """
        :type nums: List[int]
        :rtype: TreeNode
        """
        return self._build_tree(nums, 0, len(nums) - 1)
{% endhighlight %}