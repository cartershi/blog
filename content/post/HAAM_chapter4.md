---
title: "HAAM_chapter4"
date: 2019-07-11T11:37:54+08:00
draft: false
tags: ["approximation algorithm","gele"]
---

Greedy Methods

贪心方法大全

Set Cover：常用分析，charge scheme。

Shortest Superstring Problem：包含所有字符串的超串，这个问题可以常数近似。

Steiner Trees：边权版不提了，点权版每次贪心的挑选一个spider，直至全覆盖。

K-Centers：找k个中心，使得每个点到中心的最短距离都小。每次挑选一个距离当前中心最远的点加入中心。证明思路就是OPT的k个点的最优半径必然覆盖所有点，而贪心中第K+1次挑选的距离就是贪心的答案，这K+1个点必然有两个比OPT中某个点覆盖，这两点的距离两次放缩得不小于贪心的答案，再由三角不等式。

Connected Dominating Sets：

Scheduling：对于一种特殊的情况：一台机器且所有工作价值相同，一个贪心方法是挑选最早完成的工作。

Minimum-Degree Spanning Trees：在度数不超过d的情况下的最小生成树，这个问题在度的限制不放宽的情况下不可近似，但在度$O(\log n)$近似下可以得到$O(\log n)$的树。算法是不断用匹配选择度不超过d的森林拼接成树。

Maximum-Weight b-Matchings：最大权匹配，但每个点可被用b次。多项式可解但是可极快近似，对边排序，然后不断的加边。

Primal-Dual Methods：点覆盖著名应用。

Greedy Algorithms via the Probabilistic Method：组合数学利器，maxcut著名应用，独立集比较著名，接下来gele

