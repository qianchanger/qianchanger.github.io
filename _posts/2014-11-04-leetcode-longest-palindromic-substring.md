---
date: 2014-11-04
layout: post
title: "[JobHunt]leetcode - Longest Palindromic Substring "
categories: code
tags: leetcode
---

>Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.

{% highlight cpp %}
string longestPalindrome(string s) {
    int n = s.size();
    if (n <= 1) {
        return s;
    }

    int idx = 0;
    int max_len = 1;

    bool table[1000][1000] = {false};

    for (int i = 0; i < n; ++i) {
        table[i][i] = true;
    }

    for (int i = 0; i < n-1; ++i) {
        if (s[i] == s[i+1]) {
            table[i][i+1] = true;
            idx = i;
            max_len = 2;
        }
    }

    for (int len = 3; len <= n; ++len) {
        for (int i = 0; i < n-len+1; ++i) {
            int j = i+len-1;
            if (table[i+1][j-1] == true && s[i] == s[j]) {
                table[i][j] = true;
                idx = i;
                max_len = len;
            }
        }
    }

    return s.substr(idx, max_len);
}
{% endhighlight %}

---
DP解法的亮点在于两层的loop把len的增加放在外面

这样就可以直接在里面update idx和max_len了

明早起来写中心扩展的解法