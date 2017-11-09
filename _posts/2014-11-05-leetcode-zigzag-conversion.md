---
date: 2014-11-05
layout: post
title: "[JobHunt]leetcode - ZigZag Conversion "
categories: code
tags: leetcode
---

The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)
And then read line by line: "PAHNAPLSIIGYIR"

<!--more-->
{% highlight cpp %}
string convert(string s, int nRows) {
    if (nRows == 1) {
        return s;
    }

    int step = nRows*2-2;
    string ret;

    for (int i = 0; i < nRows; ++i) {
        if (i == 0 || i == nRows-1) {
            int idx = i;
            while (idx < s.size()) {
                ret.push_back(s[idx]);
                idx += step;
            }
        } else {
            int step1 = (nRows-1-i)*2;
            int step2 = step - step1;
            int idx = i;
            bool flag = true;
            while (idx<s.size()) {
                ret.push_back(s[idx]);
                if (flag)
                    idx += step1;
                else
                    idx += step2;
                flag = !flag;
            }
        }
    }

    return ret;
}
{% endhighlight %}

---
上午一题!