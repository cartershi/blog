---
title: "HAAM_chapter6"
date: 2019-07-15T20:11:12+08:00
draft: false
tags: ["approximation algorithm","gele"]
---

# Linear Programming

线性规划有两个常用的方法：rounding和dual，ruonding一般需要将整数规划用线性规划解，然后根据具体情况将分数解转化成整数解。dual是同时优化原问题和对偶问题，不要调用线性规划求解器。本章主要是rounding。

## 6.2 Rounding

需要明确的是basic feasible solution的定义，满足真正独立的有用限制的解。其实就是让变量尽可能多为0的合法解，也是simplex跑出来的结果。

**makespan：**将每个部分分配的工作匹配到一个具体的机器上即可。匹配工作到机器这件事能成立需要考虑的basic feasible solution的性质，规划中的限制最多n+m个，也就是说数组A的秩最多为n+m，所以解最多n+m个元素非0。若有k个工作被部分分配，最少在结果中占2k个位置，剩下n-k个工作占1个位置，即最少有n+k个元素非0，所有最多m个工作被部分分配。这些部分分配的工作形成pseudoforest（原因看不懂了，**坑**）。直接用LP比IP小且匹配得到2近似。
**METRIC FACILITY LOCATION：**这里考虑最简单的直接在client上建facility的情况。思路是对于所有点按它们的平均距离递增排序，然后尽可能的选4/3倍平均距离的不相交的球体。每个球体选择一个最便宜的地点开设facility，每个client选一个最近facility供应。证明第一块好像又跳了很大一部**坑**，第二部分容易理解，不过觉得8/3写成4/3了。

**GENERALIZED STEINER NETWORK：**将relax后的式子迭代的计算选取$\ge\frac{1}{2}$的边。这里有个非常复杂的证明。

## 6.3 Randomized Rounding

**MAXIMUM COVERAGE：**将LP解得的x看成选取这个集合的概率，然后以这样的概率随机取k个。对每个元素，可以得到它被覆盖的概率的下界（注意下界证明的不等式不是恒成立，而是题中范围恒成立），从而得到被覆盖的期望的下界。

**CONGESTION MINIMIZATION：**每条路径被选择的概率等于它LP的结果。得到每条边被覆盖次数的期望。还可用chernoff bound得到每条边覆盖次数的概率结果（书上又跳了一步union bound）。

## 6.4 Metric Spaces

**MINIMUM MULTICUT：**这个问题就是把k对点给割开，求最小割。$O(\log k)$的近似算法是对于每个边给一个权重，任一对点之间的任意条路劲都需要权重和$\ge1$，对这个线性规划给出一个解之后，用每条边上的权作为边权建立新图，这是k对点之间的最短路都至少为1。接着对于这2k个点中的每一个点w和一个实数$\rho$，定义$E_{\rho}$为所有的边$e=uv$，使得$d(u,w)\le\rho,d(v,w)>\rho$。构造定义$f'(\rho),f(\rho)$，保证$\exists\rho\in[0,\frac{1}{3}],f'(\rho)\le 3f(\rho)\ln k$。算法就是每个未删除的点对，选一个点，找到它对应的上述$\rho$，将所有与它距离不超过$\rho$的点一起删除，并且这样导致的割边记入cut中，这里的割边其实就是定义中的$E_{\rho}$，这样其实是删除了分支（不一定联通），由于$\rho\le\frac{1}{3}$，所以一个点对不可能被同时删除，当它们某次被分开时，一定被割开了，所以这是一个割。由于每条边最多被1次，所以对这k次割的f值求和可得不会超过规划目标得两倍，然后用f‘和f的不等式得近似比。

**SPARSEST CUT：**~~鸽了~~

**MINIMUM LINEAR ARRANGEMENT：**V个点赋予1..V的排列$\varphi$，最小化$\sum_{\{u,v\}\in E}|\varphi(u)-\varphi(v)|$。关键的发现是所谓的well spread，这个relax到一个距离度量，可以写成一个线性规划。接下来用rounding来把metric变成排列，有点像MINIMUM MULTICUT的分析，但是鸽了。