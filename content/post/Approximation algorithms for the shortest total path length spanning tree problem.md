---
title: "Approximation algorithms for the shortest total path length spanning tree problem"
date: 2019-07-25T14:51:38+08:00
draft: false
tags: ["论文学习"]
---

作者：Bang Ye Wu , Kun–Mao Chao , Chuan Yi Tang

HAAM 59章的相关内容。

## Preliminaries

**Defnition 4**. Let G =(V,E,w) and R be a tree contained in G. T is a general star of G with core R if T is a spanning tree of G and $d _T(i,R)=d_G(i,R)$ ∀i ∈ V. The set of all general stars of G with core  is denoted by star(G,R)

可以用dijkstra直接构造a general star of G with core R（从R跑的最短路）。

**Defnition 5**. Let T be a spanning tree of G, and let S be a connected subgraph of T. A branch of S is a connected component of the induced subgraph of T with vertices V(T) − V(S). Let $0<k\le2$ be a real number. If $|V(B)|\le kn$ for every branch B of S, then S is called a k-separator of T. A k-separator S is minimal if any proper subgraph of S is not a k-separator of T

树上常用定义。其他引理和定义参考HAAM 59章

## A 15/8-approximation algorithm

核心思想就是$\frac{1}{3}-$separator是一条路，而且两个端点的孩子至少$\frac{1}{3}n$，这样计算每个连通分支到其他连通分支的点的距离直接点用到separator的距离和separator之间的距离代替，separator之间的距离只考虑separator中每个点到两个端点的距离即可。从而得到lemma8，即最优解的下界。

考虑$\frac{1}{3}-$separator的两个端点的最短路R，计算$\frac{1}{3}-$separator的所有连通分支的点到R的距离，分成端点和非端点处理，可得一个不等式，然后用lemma 3直接得到这样算的上界，可得近似比。

一个$O(n^3)$的算法就是穷举一个端点m，然后$O(n^2)$计算所有点作为端点i的general star的结果。只需要计算每个点到这条路径的最短距离，可以在m的最短路径树上遍历i，这样路径的长度只需要计算到i的父亲和m的路径和i到它的距离即可。

## A 3/2-approximation algorithm

类似lemma9的证明可得穷举三元组是一个3/2近似。$O(n^4)$的算法设计也类似$O(n^3)$。

## A (4/3+$\delta$)-approximation algorithm for SPST

核心思想是建立$\frac{1}{4}-$separator，从centroid m0出发，至多三个分支，每个分支子树的centroid 为m1,m2,m3，则{m0,m1,m2,m3}在树上的最短路构成$\frac{1}{4}-$separator，称为fork-separator。

定义 Nhang(T,R,A) contains all the vertices not hung on any vertex in A，Nhang对于路径和fork还有不同的定义，要看清楚。 Lemma 15只考虑m1,m2,m3下面的点及其他的点即可即可。

Lemma 17的证明用了fork的特殊性质：三条路径拼接。所以从根做dfs，序列中连续的点最短路只能是到父亲或者到根，所以core算法不会错过。

接下来的证明就是trivial的了。

