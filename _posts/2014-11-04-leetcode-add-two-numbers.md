---
date: 2014-11-04
layout: post
title: "[JobHunt]leetcode - Add Two Numbers "
categories: code
tags: leetcode
---

>You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

<!--more-->
{% highlight cpp %}
ListNode *addTwoNumbers(ListNode *l1, ListNode *l2) {
    if (l1 == NULL)
        return l2;
    if (l2 == NULL)
        return l1;

    ListNode *head = new ListNode(-1);
    ListNode *cur = head;
    int carry = 0;

    while (l1 && l2) {
        int sum = l1->val + l2->val + carry;
        carry = sum / 10;
        ListNode *node = new ListNode(sum % 10);
        cur->next = node;
        cur = cur->next;
        l1 = l1->next;
        l2 = l2->next;
    }

    while (l1) {
        int sum = l1->val + carry;
        carry = sum / 10;
        ListNode *node = new ListNode(sum % 10);
        cur->next = node;
        cur = cur->next;
        l1 = l1->next;
    }

    while (l2) {
        int sum = l2->val + carry;
        carry = sum / 10;
        ListNode *node = new ListNode(sum % 10);
        cur->next = node;
        cur = cur->next;
        l2 = l2->next;
    }

    if (carry) {
        ListNode *node = new ListNode(carry);
        cur->next = node;
    }

    return head->next;
}
{% endhighlight %}

---

差点就忘记最后还要检查carry
