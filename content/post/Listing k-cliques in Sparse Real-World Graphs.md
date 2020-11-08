---
title: "Listing k-cliques in Sparse Real-World Graphs"
date: 2020-10-27T15:24:56+08:00
draft: false
tags: ["k-clique"]
---

本文列举真实稀疏图谱中的所有k-clique。这个问题比较常用，比如k-clique最密子图常将其作为一个subroutine。

## DEFINITIONS AND NOTATION

**arboricity**定义为将图中的边分到树，需要的最小的树个数。

**core value**定义为最大整数c，使得G中有个子图，它每个点的度都不少于c。 图的**core value**可以不断删除度数最小的点得到。**core ordering**定义为这个过程中的点序。 

定义有向图$\vec{G}$induced by the ordering$\eta$为$\vec{G}$中边$v\rightarrow u$的方向为$\eta(v)<\eta(u)$。这张图最大出度显然是core value，反证一下即可。

core ordering的优势在于出度比较小。

## ALGORITHMS

### Algorithm of Chiba and Nishizeki

按照度非递增顺序处理点，每次处理包含这个点的clique。递归处理它的邻居的导出子图中的k-1 clique。

这个算法的优势在于稀疏图上跑的很快。时间复杂度就算了。

问题在于

1. 并行
2. 度非递增顺序是否必要
3. 减少操作数

### The kClist Algorithm

算法稍微改了一下，$\vec{G}$induced by the ordering$\eta$作为输出图，不再对点排序，而是直接进行递归处理。

这里给定了全序关系，

高效实现，用标签标记每个点的版本号，版本号为$l-1$的节点将同样版本号的邻居排在邻接链表的前面。

### Efficient Parallel Algorithm

并行版本的做法是每次考虑一条边，将这两个点在一起作为clique的起点。这对并行，因为每个线程分配的任务数比每个点作为起点更均匀。

## 算法分析

比较易懂的数学归纳法，略过。

结论是Theorem 5.7，一个稍微比Chiba的bound稍微好一点的结果

