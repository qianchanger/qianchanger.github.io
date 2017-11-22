---
date: 2014-11-05
layout: post
title: "[JobHunt]leetcode - Palindrome Number "
categories: code
tags: leetcode
---

>Determine whether an integer is a palindrome. Do this without extra space.

{% highlight python %}
def isPalindrome(self, x):
    s = str(x)
    l = 0
    r = len(s) - 1
    while (l < r):
        if (s[l] != s[r]):
            return False
        l += 1
        r -= 1
    return True
{% endhighlight %}

<!--more-->

{% highlight cpp %}
bool isPalindrome(int x) {
    if (x<0)
        return false;

    if (x< 10) {
        return true;
    }

    int count = 1;
    while (x/pow(10, count-1) >= 10) {
        count++;
    }

    int l = count;
    int r = 1;

    while (l > r) {
        int l_val = getNthDigit(x, l);
        int r_val = getNthDigit(x, r);
        if (l_val != r_val) {
            return false;
        }
        l--;
        r++;
    }
    return true;
}

int getNthDigit(const int x, const int n) {
    int rem = pow(10, n);
    int div = pow(10, n-1);
    return (x % rem) / div;
}
{% endhighlight %}

---
Python的解放是作弊了 使用了extra space

需要注意的是x/pow(10, count-1) >= 10, 有等于这个case
