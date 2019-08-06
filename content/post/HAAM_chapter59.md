---
title: "HAAM_chapter7"
date: 2019-07-24T14:53:16+08:00
draft: false
tags: ["approximation algorithm","gele"]
---
本文的目标是找一棵联通树，使得$\sum_{u,v\in V}\lambda(u,v)d_T(u,v)$最小，下面称为cost，树T的cost写为c(T)。

## Minimum Routing Cost Spanning Tree

这里设置为$\lambda(u,v)=1$，所以目标变成了是找一棵联通树，cost为任两点之间的距离和。

### Shortest-Paths Trees and Solution Decomposition

做法一：取图的median r，从r开始找最短路径树。对于任意的树Y的cost小于等于2n倍所有点到根的距离和（三角不等式），这恰好median决定的东西。累加起来是图上面的两点间距离和，优于最优树上的cost。这样得到一个2近似。

做法二：基于decomposition，考虑最优树T上的centroid为根r，T的cost至少是n倍所有点到r的距离和，又由于任意树的cost小于等于2n倍所有点到根的距离和，所以以r为根的最短路径树是T的2近似。只要穷举所有的根找最小即可。

### Routing Loads, Separators, and General Stars

接下来是一堆定义，又是利用树上的性质。$l(T,e)=2x(n-x)\le2\frac{n}{2}\cdot\frac{n}{2}$，其中x是$T-e$中较小的连通分支的大小。实际上l表示两个连通分支中的点的最短路经过e的次数，所以可以得到$c(T)=\sum_{e\in T} l(T,e)w(e)$。注意所有$l$对树进行一次bfs即可得到，于是$c(T)$线性时间可以计算。

minimal δ-separator是以centroid为根的树中子树点数多余$\delta n$个的所有点形成的联通树。

**Definition 59.1** Let R be a tree contained in graph G. A spanning tree T is a general star with core R if each vertex is connected to R by a shortest path.

上面的定义不需要R是最短路径树。

**Lemma 59.3** If T is a general star with core S, $c(T)\le 2n\sum_{v\in V}d_{G}(v,S)+\frac{n^2}{2}w(S)$

**Lemma 59.4** If S is a minimal δ-separator of $\hat T$, then 

$c(\hat T)\ge 2(1-\delta)n\sum_{v\in V}d_{\hat T}(v,S)+2\delta(1-\delta)n^2w(S)$

trivial的结论。注意当$\delta=\frac{1}{2}$，则$S=\{r\}$，实际上就是上一节的做法二。以上两条lemma导出相面的两个算法。

### Approximating by a General Star

当$\delta=\frac{1}{3}$，注意每个孩子都最多$\frac{1}{2}n$节点，所以separator中每个孩子最多只有一个孩子，而根最多有两个孩子，所以这个δ-separator是路径。

算法一：穷举所有的点对，用它们的最短路作为δ-separator生成general star 找最小的一颗可证近似比为$\frac{18}{5}$。

算法二：穷举三元组，用经过三点的最短路作为δ-separator生成general star 可证近似比为$\frac{3}{2}$。

细节见Approximation algorithms for the shortest total path length spanning tree problem

### A Reduction to the Metric Case

当$\delta=\frac{1}{4}$时，近似理论上可以做到$\frac{4}{3}$（直接比较lemma 59.3 59.4）,由于general star的限制，这个近似比无法被改进。metric closure就是常用的概念，在边权满足metric的条件下的近似算法可以解决补满足的情况，并且近似比不变差。

定义k-star为中间节点最多为k个的树。

### A Polynomial-Time Approximation Scheme

参见A POLYNOMIAL-TIME APPROXIMATION SCHEME FOR MINIMUM ROUTING COST SPANNING TREES。

## Product-Requirement Communication Spanning Tree

### Approximating by 2-Stars

思路还是与MRCT一样，借助routing cost的定义可以式59.1，每个点往x连第三项的值，往y连第二项的值，两点之间连第一项的值，在这张图上找x、y的最小割即可得到最小值。

### A Polynomial-Time Approximation Scheme

与MRCT不同的是不能在多项式时间内寻找最好的k-star。所以将一部分较大的点权进行缩小成整数，对这些点复制点权次，跑MRCT。小的点直接连接到靠近的点。

## Sum-Requirement Communication Spanning Tree

依然是变换routing cost的定义，定义为$l_s(T,e)=2(r(T_u)|V(T_v)|+r(T_v)|V(T_u)|)$，依然有$c(T)=\sum_{e\in T} l_s(T,e)w(e)$，这个问题和前两个的不同在于不能单纯用metric closure的情况处理，因为有可能导致结果变小。

算法是对每个点找最短路径树，cost最小得就是答案。

由$l_s(T,e)=(|V(T_v)|-\frac{n}{2})(r(T_u)-\frac{R}{2})+(|V(T_u)|-\frac{n}{2})(r(T_v)-\frac{R}{2})+\frac{nR}{2}$得从centroid到r-centroid的路径中的$l_s(T,e)\ge\frac{nR}{2}$，然后分析得lemma59.9。

依然对分类可得2近似。~~坑~~

## Multiple Sources MRCT

p-MRCT是SROCT的特殊情况，所以可以2近似。

### Approximating the 2-MRCT

对于只有两个点算数的情况，考虑最优解：对于每个点到两个目标的树上距离，均$\ge$图上距离，取出一半用三角不等式，得式(59.4)；在考虑算法的近似比：对于每个点到两个目标的树上距离，等于2倍到路径的距离+路径的距离，到路径的距离转化为到两个端点的距离。这就是一个2近似。

PTAS的思路还是一样的，穷举路径中的k个点，证明存在k个点的路径构造出来的树近似比很小。

可以证明非metric graph依适用

### The Weighted 2-MRCT

不同在于每个点要选到s1,s2谁的代价小。最后将s1,s2两棵树连接。metric graph依然穷举k个点。

## Multiple Sources OCT

### The p-OCT on Metric Graphs

对于2-OCT，类似W2MRCT处理

对于p-OCT，穷举所有的reduced skeleton。

### The 2-OCT on General Graphs

2MRCT的算法是3近似。

先记这么多吧，以后用得到再看细节。