---
date: 2015-01-25
layout: post
title: "[JobHunt]leetcode - Largest Number "
categories: code
tags: leetcode
---

题目连接点击:[这里](https://oj.leetcode.com/problems/largest-number/)

{% highlight cpp %}
static bool compfunc(const string &s1, const string &s2)
{
    return s1 + s2 > s2 + s1;
}

string largestNumber(vector<int> &num)
{
    vector<string> arr;
    for (auto i : num) {
        arr.push_back(to_string(i));
    }
    sort(arr.begin(), arr.end(), compfunc);
    string res;
    for (auto s : arr) {
        res += s;
    }
    while (res[0] == '0' && res.length() > 1) {
        res.erase(0, 1);
    }
    return  res;
}
{% endhighlight %}