---
date: 2014-11-12
layout: post
title: "[JobHunt]leetcode - Regular Expression Matching "
categories: code
tags: leetcode
---

>Implement regular expression matching with support for '.' and '*'.

{% highlight cpp %}
bool isMatch(const char *s, const char *p) {
    string s_str(s);
    string p_str(p);

    vector<vector<bool> > table(
    	p_str.size()+1,
    	vector<bool>(false, s_str.size()+1)
    );

    table[0][0] = true;

    // horizontal
    for (int i = 1; i <= s_str.size(); ++i) {
        table[0][i] = false;
    }

    // vertical
    for (int i = 1; i <= p_str.size(); ++i) {
        if (p_str[i-1] == '*') {
            table[i][0] = table[i-2][0];
        } else {
            table[i][0] = false;
        }
    }

    // DP
    for (int i = 1; i <= p_str.size(); ++i) {
        for (int j = 1; j <= s_str.size(); ++j) {
            if (p_str[i-1] == '.' || p_str[i-1] == s_str[j-1]) {
                table[i][j] = table[i-1][j-1];
            } else if (p_str[i-1] == '*') {
                table[i][j] = table[i-2][j] || (
                	table[i][j-1] &&
                	(p_str[i-2] == s_str[j-1] || p_str[i-2] == '.'));
            } else {
                table[i][j] = false;
            }
        }
    }
    return table[p_str.size()][s_str.size()];
}
{% endhighlight %}

---
因为Hackathon的缘故 刷题几乎停了一个礼拜