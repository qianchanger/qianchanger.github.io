---
date: 2014-11-04
layout: post
title: "[JobHunt]leetcode - Two Sum "
categories: code
tags: leetcode
---

题目连接点击:[这里](https://oj.leetcode.com/problems/two-sum/)

<!--more-->
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

再看看自己的code 发现最后的线性查找会花很多时间 不如这个代码简洁高效
{% highlight cpp %}
vector<int> twoSum(vector<int> &numbers, int target)
{
    unordered_map<int, int> loc;
    for (int i = 0; i < numbers.size(); ++i) {
        loc[numbers[i]] = i;
    }
    vector<int> ret;
    for (int i = 0; i < numbers.size(); ++i) {
        int v = target - numbers[i];
        if (loc.count(v) && loc[v] != i) {
            ret.push_back(i + 1);
            ret.push_back(loc[v] + 1);
            break;
        }
    }
    return ret;
}
{% endhighlight %}

---

磨蹭了半天 终于还是开始动笔刷题了
