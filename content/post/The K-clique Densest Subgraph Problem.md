---
title: "The K-clique Densest Subgraph Problem"
date: 2020-12-12T21:40:56+08:00
draft: false
tags: ["densest subgraph"]
---

本文先考虑最密三角形问题，提出它的精确算法、近似算法和mapreduce算法。然后把这些算法拉到k-clique下

## 三角形最密子图

### 精确算法

基于网络流的算法过于套路，略

基于supermodular function的方法直接证明$t(S)-\alpha|S|$是supermodular function，接着binary search$\alpha$即可。

### $\frac{1}{3}$近似算法

算法：不断的从删除三角形度最小的点。

近似比：考虑最优结果中第一个节点被删除的时刻即可

### MapReduce版

算法：每次用图中删除三角形度小于等于$3(1+\epsilon)\tau(S)$的点。

正确性：首先每次必然会删除点，否则double counting三角形个数得到矛盾。接着考虑最优结果中第一个节点被删除的时刻即得近似比。log轮证明依然double counting三角形个数。

## k-clique最密子图

trivial