---
date: 2014-11-05
layout: post
title: "[JobHunt]leetcode - String to Integer (atoi) "
categories: code
tags: leetcode
---

>Implement atoi to convert a string to an integer.

{% highlight cpp %}
int atoi(const char *str) {
    if (!str) {
        return 0;
    }

    while (*str == ' ' && str != NULL) {
        str++;
    }

    if (!str) {
        return 0;
    }

    bool flag = true;
    if (*str == '-' || *str == '+') {
        if (*str == '-') {
            flag = false;
        }
        str++;
    }

    int ret = 0;
    while (str != NULL) {
        int val = (*str) - '0';
        if (val < 0 || val > 9) {
            return ret;
        }
        if (flag) {
            if ((INT_MAX - val < ret*10) || (INT_MAX/10 < ret)) {
                return INT_MAX;
            }
            ret = 10 * ret + val;
        } else {
            if ((INT_MIN + val > ret*10) || (INT_MIN/10 > ret)) {
                return INT_MIN;
            }
            ret = 10 * ret - val;
        }
        str++;
    }
    return ret;
}
{% endhighlight %}