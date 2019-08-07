---
title: "Approximation Algorithms for Problems Combining Facility Location and Network Design"
date: 2019-08-07T14:08:38+08:00
draft: false
tags: ["论文学习","gele"]
---

作者：R. Ravi, Amitabh Sinha

## The Capacitated-Cable Facility Location Problem

### Problem Definition

这个问题CCFL是给定一个metric图，一个client集合D，一个potential facility集合F，目标是选中一些facility，每个client有一个单位的流通过图流到某个开放的facility。另外有一个整数u，表示每条边上的流不能超过u，否则就需要拷贝这条边支持流。

### Lower Bounds

Lemma 1的意思是将每条边的权重除以u作为uncapacitated facility location问题UFL，那么显然CCFL的最优解是可以作为UFL的一个解，且它的权重比CCFL里更小，所以UFL的最优解是CCFL的下界。

Lemma 2的意思是将F连向一个超点，边权是开放facility的代价。计算超点与D的steiner树ST，CCFL的最优解显然是ST的一个解，所以ST最优解也是CCFL的下界。

### Algorithm

首先跑lemma1和lemma2的结果，将这两个算法使用的facility全部打开，然后在ST的树T上进行调整：对T从叶子到根倒顺序考虑，对于每个流量超过u的点v（记流量为$D_v$），进行调整使得v的流量不超过u。对于每个v的子树，挑选节点到facility最近的点，这些节点中选$\lfloor D_v/u\rfloor$，由于v是倒序的第一个，所以v的所有孩子流量不超过u，即每个子树的流量都不违反结果。剩下每个选中的子树需要连接到v或者另一棵子树使得新装的路径被填满（先跑到根，在跑到对应的新子树）。~~好长的算法~~

### Analysis

UFL每个client都有到已开facility的最短距离，新开的路是u个client中最小的，所以填满以后的权重小于这些点在UFL中的代价。唯一需要注意的是从其他子树拉过来填充的点会用掉它到v的流量，这样下一次产生矛盾时直接取消这个流并将其导入这个流流入的子树即可。

所以这样是feasible solution且不会超过ST+UFL的近似解，再由lemma1和2得近似比。

### IP Formulation and Its Gap

~~坑~~

### Nonuniform Demands

这个情况下每个点的流为$d_i$而不是1。对于$d_i\ge u$，直接将其分配给UFL最近的facility，这是UFL的近似算法的2近似；对于$d_i<u$，将流装到$[u,2u]$，这样是2近似。得到结论。

对于流可分的情况，完全可用Nonuniform的算法，所以近似比不变。

## The Capacitated-Cable p-Median Problem

CCpM问题开facility无代价，但是不能打开超过p个facility。这是一个bicriteria approximation问题，$(\alpha,\beta)$近似是使用不超过$\beta p$个facility的情况下，代价不超过p个facility时的最优解的$\beta$倍。

### Overview of Our Approach

先考虑这样一个情况，每个点都是client且是potential facility。

将边权除以u得到p-median问题，这是CCpM的下界。将最小生成树最重的p-1条边删除得到的树也是CCpM的下界。接下来算法一样，在第二个得到的森林上借助p-median的结果调整。这就得到了$(\rho_{p-median}+ 1,2)$近似。

### Unrestricted Version of CCpM

这是第二个下界变成了p-Steiner forest，这个问题有一个2近似的算法~~坑~~，这就得到了$(\rho_{p-median}+ 2,2)$近似。