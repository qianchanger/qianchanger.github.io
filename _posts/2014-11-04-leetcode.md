---
date: 2014-11-04
layout: post
title: "[JobHunt]leetcode - Two Sum "
categories: code
tags: leetcode
---

>Given an array of integers, find two numbers such that they add up to a specific target number.

{% highlight cpp %}
vector<int> twoSum(vector<int> &numbers, int target) {
    vector<int> numbers_bk(numbers);
    sort(numbers.begin(), numbers.end());
    int l = 0;
    int r = numbers.size() - 1;
    while (l < r) {
        int sum = numbers[l] + numbers[r];
        if (sum == target) {
            vector<int> ret;
            for (int i = 0; i < numbers_bk.size(); ++i) {
                if ((numbers_bk[i] == numbers[l]) ||
                    (numbers_bk[i] == numbers[r])) {
                    ret.push_back(i+1);
                    if (ret.size() == 2) {
                        return ret;
                    }
                }
            }
        } else if (sum <= target) {
            l++;
        } else {
            r--;
        }
    }
}
{% endhighlight %}

---

磨蹭了半天 终于还是开始动笔刷题了