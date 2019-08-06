---
title: "On the intercluster distance of a tree metric"
date: 2019-08-06T20:13:04+08:00
draft: false
tags: ["论文学习"]
---

作者：Bang Ye Wu 

## Introduction

定义$\mu_G(V_1,V_2)=(V_1V_2)^{-1}\sum_{u\in V_1}\sum_{v\in V_2}d_G(u,v)$为两个给定点集的平均距离，目标是找到找个一棵树，使得这个值最小。

## Distance between two clusters

定义$W_G(f,h)=\sum_{u,v\in V(G)}f(u)h(v)d_G(u,v)$，建立一棵树最小化这个目标，为图中任意两点间的加权距离，即~~Product-Requirement Communication Spanning Tree~~。

定理1的证明直接做差，然后证明不断将边变为0导致$\Delta$不会变小，在最后边全为0时$\Delta=0$得证。

Corollary 4就是常用$min\{u,v\}\le xu+(1-x)v$，代入Corollary 2即可。

## The minimum average intercluster distance spanning tree

算法就是对于$V_1\cup V_2$里的所有点跑一遍最短路，取平均距离最小的。

方法就是对于$V_1$里的点算以它为根的距离上界，对于$V_2$里的点算以它为根的距离上界，各取平均距离的平均得2近似。

## Concluding remarks

类似的，若给定k个点集，算任两点的平均距离，依然可用上面的算法2近似。