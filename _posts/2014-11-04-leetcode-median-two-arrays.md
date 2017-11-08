---
date: 2014-11-04
layout: post
title: "[JobHunt]leetcode - Median of Two Sorted Arrays "
categories: code
tags: leetcode
---

>There are two sorted arrays A and B of size m and n respectively. Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

<!--more-->
{% highlight cpp %}
double findMedianSortedArrays(int A[], int m, int B[], int n) {
    if (m < n)
        return getMedianSortedArrays(A, m, B, n);
    return getMedianSortedArrays(B, n, A, m);
}

double getMedianSortedArrays(int A[], int m, int B[], int n) {
    if (m == 0) {
        if (n & 1)
            return B[n/2];
        return medianOfTwo(B[n/2], B[n/2-1]);
    }

    if (m == 1) {
        if (n == 1) {
            return medianOfTwo(A[0], B[0]);
        }

        int idx = n / 2;
        if (n & 1) {
            return medianOfTwo(
                B[idx],
                medianOfThree(A[0], B[idx-1], B[idx+1])
            );
        }

        return medianOfThree(A[0], B[idx-1], B[idx]);
    }

    if (m == 2) {
        if (n == 2) {
            return medianOfFour(A[0], A[1], B[0], B[1]);
        }

        int idx = n/2;
        if (n & 1) {
            return medianOfThree(
                B[idx],
                max(A[0], B[idx-1]),
                min(A[1], B[idx+1])
            );
        }

        return medianOfFour(
            B[idx],
            B[idx-1],
            max(A[0], B[idx-2]),
            min(A[1], B[idx+1])
        );
    }

    int idxA = (m-1) / 2;
    int idxB = (n-1) / 2;

    if (A[idxA] > B[idxB]) {
        return getMedianSortedArrays(A, m/2 + 1, B+idxA, n-idxA);
    }

    return getMedianSortedArrays(A+idxA, m/2 + 1, B, n-idxA);

}

double medianOfTwo(const int A, const int B) {
    return (A+B) / 2.0;
}

double medianOfThree(const int A, const int B, const int C) {
    return A + B + C - max(A, max(B, C)) - min(A, min(B, C));
}

double medianOfFour(const int A, const int B, const int C, const int D) {
    int Max = max(A, max(B, max(C, D)));
    int Min = min(A, min(B, min(C, D)));
    return (A + B + C + D - Max - Min) / 2.0;
}
{% endhighlight %}

---

真是一道难题 Base Case很多 具体的处理还要再记一下
