---
date: 2014-11-13
layout: post
title: "[JobHunt]leetcode - Letter Combinations of a Phone Number "
categories: code
tags: leetcode
---

>Given a digit string, return all possible letter combinations that the number could represent.

{% highlight cpp %}
vector<string> letterCombinations(string digits) {
    map<char, string> table;
    table['1'] = "";
    table['2'] = "abc";
    table['3'] = "def";
    table['4'] = "ghi";
    table['5'] = "jkl";
    table['6'] = "mno";
    table['7'] = "pqrs";
    table['8'] = "tuv";
    table['9'] = "wxyz";

    vector<string> ret;
    letterCombinations(ret, table, digits, "", 0);
    return ret;
}

void letterCombinations(vector<string> &ret, const map<char, string> &table,
                        const string &digits, string cur_str, const int cur_pos) {
    if (cur_pos >= digits.size()) {
        ret.push_back(cur_str);
        return;
    }

    char c = digits[cur_pos];
    string candidates = table.at(c);
    for (int i = 0; i < candidates.size(); ++i) {
        letterCombinations(ret, table, digits, cur_str+candidates[i], cur_pos+1);
    }
}
{% endhighlight %}