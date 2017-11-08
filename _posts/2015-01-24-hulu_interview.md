---
date: 2015-01-24
layout: post
title: "Hulu 面试笔记"
categories: code
tags: 面试
---

#面试结果   
周一飞赴洛杉矶 周二面试 周三拿到offer通知   
给Hulu HR办事效率点个赞   
<!--more-->
整个面试过程 等待的时间不超过两天   

#面试过程   

##第一轮 online coding challenge   

>读取csv文件 为公司级别列表 按照级别层次打印输出   
>code是很简单的记录深度的递归调用   

##第二轮 电面   

>问如何用一个magazine(string)来做anonymous ransom note(string)   
>就是扫一遍note 记录每个letter次数   
>再扫一遍magazine 看够不够用   
>给出code之后 被问到design question 设计一个url shortener   
>作为开放性题目   
>和面试官聊到了的技术有 hash, hdfs的读取策略, reed solomon code等   

##第三轮 Onsite   
>从上午11:30 到下午4:00 包含4个面试官   
>是我第一次Onsite经历 最后很是有点精疲力尽   

###第一面试官:   

>有一堆batch log 空格为分隔符 形式为   
>START TYPE ID   
>END ID TIME   
>求K个耗时最长的batch的种类   
>每种batch只记录其最长耗时那一个   
>follow up问题是    
>若改成实时返回最长的K个batch   
>变成online algorithm该怎么做   

###第二面试官:   

>Given BST preorder & inorder, recover BST   
>标准Leetcode题目 秒给答案   
>然后花了大量时间讨论Ads team的一些batch设计问题   
>面试官是Hulu Ads最早的工程师之一   

###第三面试官:   

>假设有一种语言 使用的是和英文一样的字母表 但字母顺序不同   
>有一本这种语言的字典 但残缺不全   
>使用字典作为输入 返回字母正确顺序   
>给出code后    
>面试官提点这道题其实可以用topological sort解决   
>感觉此人谈话风格应该是某team tech leader   

###第四面试官:   

>输入xml格式文件 输出hashtable   
>关键点在于用stack记录深度   
>此面试官是internal support team tech leader   

#面试总结
面试到后半段因为没有好好吃午饭 体力明显跟不上 思维已经断掉了   
以后不管面试中间如何紧张 导致没有食欲 都要尽量多吃一些   
下半段可以吃一点香蕉葡萄这样高血糖食物   

此外公司包机票酒店租车吃饭等一切费用 果然是很爽的   
Hulu良心公司 酒店是santa monica海滩边精品酒店海景房   
离开洛杉矶前和A神用餐补饱餐一顿不能更赞   
