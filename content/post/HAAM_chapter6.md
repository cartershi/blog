---
title: "HAAM_chapter6"
date: 2019-07-15T20:11:12+08:00
draft: true
tags: ["approximation algorithm","gele"]
---

# Linear Programming

毒瘤书又开始狂跳步骤了，慢慢写吧

线性规划有两个常用的方法：rounding和dual，ruonding一般需要将整数规划用线性规划解，然后根据具体情况将分数解转化成整数解。dual是同时优化原问题和对偶问题，不要调用线性规划求解器。本章主要是rounding。

## 6.2 Rounding

需要明确的是basic feasible solution的定义，满足真正独立的有用限制的解。其实就是让变量尽可能多为0的合法解，也是simplex跑出来的结果。

**makespan：**将每个部分分配的工作匹配到一个具体的机器上即可。匹配工作到机器这件事能成立需要考虑的basic feasible solution的性质，规划中的限制最多n+m个，也就是说数组A的秩最多为n+m，所以解最多n+m个元素非0。若有k个工作被部分分配，最少在结果中占2k个位置，剩下n-k个工作占1个位置，即最少有n+k个元素非0，所有最多m个工作被部分分配。这些部分分配的工作形成pseudoforest（原因看不懂了，**坑**）。直接用LP比IP小且匹配得到2近似。
**METRIC FACILITY LOCATION：**这里考虑最简单的直接在client上建facility的情况。思路是对于所有点按它们的平均距离递增排序，然后尽可能的选4/3倍平均距离的不相交的球体。每个球体选择一个最便宜的地点开设facility，每个client选一个最近facility供应。证明第一块好像又跳了很大一部**坑**，第二部分容易理解，不过觉得8/3写成4/3了。

**GENERALIZED STEINER NETWORK：**将relax后的式子迭代的计算选取$\ge\frac{1}{2}$的边。这里有个非常复杂的证明。

## 6.3 Randomized Rounding

**MAXIMUM COVERAGE：**将LP解得的x看成选取这个集合的概率，然后以这样的概率随机取k个。对每个元素，可以得到它被覆盖的概率的下界（注意下界证明的不等式不是恒成立，而是题中范围恒成立），从而得到被覆盖的期望的下界。

**CONGESTION MINIMIZATION：**每条路径被选择的概率等于它LP的结果。得到每条边被覆盖次数的期望。还可用chernoff bound得到每条边覆盖次数的概率结果（书上又跳了一步union bound）。

6.4 Metric Spaces

