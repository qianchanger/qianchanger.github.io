---
date: 2015-01-14
layout: post
title: "[JobHunt]leetcode - Word Ladder II "
categories: code
tags: leetcode
---

Given two words (start and end), and a dictionary, find all shortest transformation sequence(s) from start to end, such that:   

Only one letter can be changed at a time   
Each intermediate word must exist in the dictionary   
For example,   

Given:   
start = "hit"   
end = "cog"   
dict = ["hot","dot","dog","lot","log"]   
Return
>  [
>    ["hit","hot","dot","dog","cog"],
>    ["hit","hot","lot","log","cog"]
>  ]

{% highlight cpp %}
vector<vector<string>> findLadders(string start, 
                                   string end, 
                                   unordered_set<string> &dict
) {
    vector<vector<string> > ret;
    vector<string> path;
    dict.erase(start);
    path.push_back(start);
    find_ladder(ret, path, start, end, dict);
    return ret;
}

void find_ladder(vector<vector<string> > &ret, 
                 vector<string> &path, 
                 string &cur_word,
                 const string &end,
                 unordered_set<string> &dict
) {
    if (cur_word == end) {
        if (ret.empty() || path.size() < ret[0].size()) {
            ret.clear();
            ret.push_back(path);
        } else if (path.size() == ret[0].size()) {
            ret.push_back(path);
        }
        return;
    }
    
    for (int i = 0; i < cur_word.size(); ++i) {
        char c = cur_word[i];
        for (char x = 'a'; x <= 'z'; ++x) {
            cur_word[i] = x;
            if (dict.count(cur_word)) {
                path.push_back(cur_word);
                dict.erase(cur_word);
                find_ladder(ret, path, cur_word, end, dict);
                dict.insert(cur_word);
                path.pop_back();
            }
        }
        cur_word[i] = c;
    }
}
{% endhighlight %}
LTE