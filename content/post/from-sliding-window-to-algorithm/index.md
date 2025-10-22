---
title: From Sliding Window to Algorithm
description: A concise guide to sliding window techniques — fixed and dynamic
  windows, core ideas, algorithmic patterns, and practical examples for
  efficient array and substring problem solving.
date: 2025-10-22T16:39:00.000+08:00
image: sliding-window.jpg
categories:
  - Algorithm
weight: 1
---
滑动窗口（Sliding Window）是在面对数组和字符串题目时常见的方法与思路，在面对“具有某种特征的子区间”相关问题处理时尤其有效。其核心思想是在序列上维护一个**“窗口”**，“窗口”内包含的是满足题目特征的子序列。通过“窗口”的滑动，实现对序列的快速遍历与处理。这里的处理通常指的是针对于具有某种特征的子序列的查找。因而，解决**具有某种特征的连续子序列查找问题**是滑动窗口方法主要的应用，而这也是数组和字符串题目的一大重点内容。

例如，在题目[3090. 每个字符最多出现两次的最长子字符串](https://leetcode.cn/problems/maximum-length-substring-with-two-occurrences/)中，“每个字符最多出现两次”就是题目对于子序列的要求，需要做的就是遍历查找这样的子序列的最大长度。

滑动窗口方法通常分为**定长滑动窗口**和**动态滑动窗口**两种基本窗口模式，题目中会以明确的子序列长度限制进行区分。前者相对更简单，一般只需要滑动定长窗口，对窗口内元素进行统计；后者由于窗口长度动态，涉及窗口内元素的动态添加与移除，但也有相对固定的模式和框架可以进行总结。

本文剩下部分将从定长滑动窗口、动态滑动窗口两种基本窗口模式入手，分别介绍其基本思路、算法框架与例题。

# 定长滑动窗口





# 动态滑动窗口





## 求子序列最长/最大



## 求子序列最短/最小



## 求子数组个数

