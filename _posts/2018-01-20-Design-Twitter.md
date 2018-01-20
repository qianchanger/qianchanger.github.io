---
date: 2018-01-20
layout: post
title: "[JobHunt]leetcode - Design Twitter "
categories: code
tags: leetcode
---

https://leetcode.com/problems/design-twitter/description/   

这题目要AC是非常容易的 因为我感觉自己的design问题很大 居然也过了   
不过这是很好的一个契机 去了解一下真实的weibo newsfeed是怎么设计的   
https://www.zhihu.com/question/19645686   

<!--more-->

题目代码如下

{% highlight python %}
class Twitter(object):

    def __init__(self):
        import collections
        # key: user, value: the users who the key user is following
        self.follower_map = collections.defaultdict(set)  
        # key: user, value: the users who the key user is followed by
        self.followee_map = collections.defaultdict(set)  
        # key: user, value: the top 10 twitts a user should see
        self.user_twitts = collections.defaultdict(list)   
        

    def postTweet(self, userId, tweetId):
        import time
        self.user_twitts[userId].append(
            (time.time(), tweetId)
        )

    def getNewsFeed(self, userId):
        import copy
        tweetIds = copy.copy(self.user_twitts[userId])
        for f in self.follower_map[userId]:
            tweetIds.extend(self.user_twitts[f][-10:])
        
        # sort
        tweetIds = sorted(tweetIds, key=lambda x: x[0])[-10:]
        tweetIds = [x[1] for x in reversed(tweetIds)]
        
        return tweetIds

    def follow(self, followerId, followeeId):
        if followerId == followeeId:
            return
        self.follower_map[followerId].add(followeeId)
        self.followee_map[followeeId].add(followerId)

    def unfollow(self, followerId, followeeId):
        self.follower_map[followerId].discard(followeeId)
        self.followee_map[followeeId].discard(followerId)
{% endhighlight %}