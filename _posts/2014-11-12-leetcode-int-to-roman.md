---
date: 2014-11-12
layout: post
title: "[JobHunt]leetcode - Integer to Roman "
categories: code
tags: leetcode
---

Given an integer, convert it to a roman numeral.
Input is guaranteed to be within the range from 1 to 3999.

<!--more-->
{% highlight cpp %}
string intToRoman(int num) {
    char sym[7] = {'I', 'V', 'X', 'L', 'C', 'D', 'M'};
    string ret;
    int scale = 1000;
   for (int i = 6; i >= 0; i -= 2) {
        int v = num / scale;
        if (v != 0) {
            if (v <= 3) {
                ret.append(v, sym[i]);
            } else if (v == 4) {
                ret.append(1, sym[i]);
                ret.append(1, sym[i+1]);
            } else if (v == 5) {
                ret.append(1, sym[i+1]);
            } else if (v <= 8) {
                ret.append(1, sym[i+1]);
                ret.append(v-5, sym[i]);
            } else {
                ret.append(1, sym[i]);
                ret.append(1, sym[i+2]);
            }
        }
        num = num % scale;
        scale /= 10;
    }
    return ret;
}
{% endhighlight %}