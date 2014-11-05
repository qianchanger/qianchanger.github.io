---
date: 2014-11-04
layout: post
title: "[JobHunt]leetcode - Longest Substring Without Repeating Characters "
categories: code
tags: leetcode
---

>Given a string, find the length of the longest substring without repeating characters. For example, the longest substring without repeating letters for "abcabcbb" is "abc", which the length is 3. For "bbbbb" the longest substring is "b", with the length of 1.

{% highlight cpp %}
int lengthOfLongestSubstring(string s) {
    int max_length = 0;
    int cur = 0;
    map<char, int> location;
    for (int i = 0; i < s.size(); ++i) {
        map<char, int>::iterator it = location.find(s[i]);
        if (it != location.end()) {
            cur = max(cur, it->second + 1);
        }
        location[s[i]] = i;
        max_length = max(max_length, i - cur + 1);
    }
    return max_length;
}
{% endhighlight %}

---
一个记录位置的map罢了 这题还是很直观的