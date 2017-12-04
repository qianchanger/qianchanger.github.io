---
date: 2017-12-03
layout: post
title: "[JobHunt]leetcode - Word Break I & II  "
categories: code
tags: leetcode
---

https://leetcode.com/problems/word-break/description/   
https://leetcode.com/problems/word-break-ii/description/   

最直观的思路是   

<!--more-->

{% highlight python %}

def wordBreak(s, wordDict):
    for i in range(len(s) + 1):
        if s[:i] in wordDict and wordBreak(s[i:], wordDict):
            return True
    return False

{% endhighlight %}

但是显然这样会超时 因为有很多重复的计算   
比如\\(i=i_n\\)的时候计算了后面\\(i_n\\)之后的substring可不可以分   
当\\(i=i_{n+1}\\)的时候 又会计算一遍前面已经计算过的substring的子集   
对于这种\\(i_{n-1}\\)可以帮助求解\\(i_n\\)的问题 DP是显而易见的解决方法   
所以有解法   

{% highlight python %}
    def wordBreak(self, s, wordDict):
        """
        :type s: str
        :type wordDict: List[str]
        :rtype: bool
        """
        wordDict = set(wordDict)
        valid = [True]
        for i in range(1, len(s) + 1):
            valid.append(any(valid[j] and s[j:i] in wordDict for j in range(i)))
        return valid[-1]
{% endhighlight %}

对于第二问 只需要把前面的sub solution保存下来就行了

{% highlight python %}
    def wordBreak(self, s, wordDict):
        """
        :type s: str
        :type wordDict: List[str]
        :rtype: List[str]
        """
        solutions = {
            0: []
        }

        def solve(i):
            for j in range(i):
                if s[j:i] in wordDict:
                    if j == 0:
                        current_j_solution = [s[:i] + ' ']
                    else:
                        current_j_solution = [elem + s[j:i] + ' ' for elem in solutions.get(j, [])]

                    if i not in solutions:
                        solutions[i] = current_j_solution
                    else:
                        solutions[i].extend(
                            current_j_solution
                        )

        for i in range(1, len(s) + 1):
            solve(i)
        
        result = [elem.strip() for elem in solutions.get(len(s), [])]
        return result
{% endhighlight %}