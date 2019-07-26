---
title: "A tight bound on approximating arbitrary metrics by tree metrics"
date: 2019-07-09T20:57:35+08:00
draft: false
tags: ["论文学习","gele"]
---

作者：Jittat Fakcharoenphol, Satish Rao and Kunal Talwar

## The algorithm

**定义**：首先将最短距离扩大到至少为1，定义$\Delta=2^\delta$为直径的上界，度量d'支配d表示任两点d'>d，本文的目标即寻找树上的度量d‘，它支配真正的距离d，并且d’的期望距离$\le\alpha d(u,v)$，这称为$\alpha$概率近似。r-cut定义为以某个点为中心的半径为r的cluster，$D_i$为$D_{i+1}$的$2^i$-cut。

**算法**：首先随机产生n个点的排列，以$p(x)=\frac{1}{x\ln2}$的概率挑选$\beta\in[1,2]$，若当前集合中元素不止一个，将每个元素分配给排列中第一个距离小于$2^{i-1}\beta$的点。这显然是形成了树中节点的孩子，边权为$2^i\ge 2^{i-1}\beta$，大于等于当前点的半径。

**支配**：两点u,v的距离就是两点在树中对应的叶子节点之间的距离。考虑它们的LCA x，注意在树上u到x的距离至少是x的半径（这里有两次放缩），x在图上这个半径包含u，所以$d(u,x)\le d^T(u,x)$，三角不等式可得以树作为度量支配图的距离。

**$\alpha$概率近似**：Observation1通过简单的变量替换即可得到，若$LCA(u,v)=x$在第i层，则$d^T(u,x)<2^{i+1}$，所以$d^T(u,v)<2^{i+2}\le8\beta_i$。将随机排列的n个点按照$\min(d(u,w),d(v,w))$从小到大排序，得$E[d^T(u,v)]\le \sum_i E[d^T_{w_i}(u,v)]$，$d^T_{w_i}(u,v)$表示为$w_i$将它们分割的情况下的距离。注意到$w_i$将它们分割时$w_i$必然在前$i-1$个点的前面，否则这些点会将u,v直接分开或者带入更小的集合，由于随机排列，这样的概率为$\frac{1}{i}$。对所有可能的$\beta_i$做积分求期望（这边也有点绕，并不是直接对$\beta$积分），外面再乘一个$\frac{1}{i}$即可求出$E[d^T_{w_i}(u,v)]$，最后直接累加。~~天才般的证明~~

## Derandomization

~~鸽了~~