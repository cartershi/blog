---
title: "An improved approximation algorithm for the 0-extension problem"
date: 2019-07-21T14:24:25+08:00
draft: false
tags: ["论文学习"]
---

作者：Jittat Fakcharoenphol, Chris Harrelson, Satish Rao, Kunal Talwar

## Introduction

本问题是将每个点映射到给定的terminal上，使得原来有边的任两点之间的距离和与现在距离和之间近似比尽可能小。

这篇文章有一个漂亮的relaxation，它relax出一个新的semimetric度量，只保证terminal之间的距离不变即可。

## Notation

定义$A_u$为u最近的terminal或者到它的距离。显然每个点挑选$A_u$是不合理的，因为terminal之间的距离可能是$O(A_u)$级别的，若$d(u,v)$很小，则无法很好的近似。

## The CKR algorithm

随机一个terminal的排列，选择一个$[1,2)$的数$\alpha$，每个点u赋值给排列中第一个距离小于$\alpha A_u$的的点。

对于目标函数的两点距离，$\delta(f(u),f(v))\le\delta(f(u),u)+\delta(u,v)+\delta(f(v),v)$直接可以解决前两种情况。否则需要一个概率的证明（参见CKR的证明）：考虑u，v被分开的概率，等价于u被m$(\alpha)$中的点覆盖，而v一定被$s(\alpha)$覆盖，由于排列得随机性，得$P[\epsilon(u,v)|\alpha]\le\frac{m(\alpha)}{m(\alpha)+s(\alpha)}$，对$\alpha$求积分得基本就解决了。为了解决积分的问题，需要对积分式做归纳，也很简单。

## Our algorithm

不同在于随机变量，挑选一个$\gamma\in[1,2]$，设置$A_v'=\min\{2^s:2^s\ge2A_v/\gamma\}$（图中最短距离被扩大到1），随机挑选一个$i\in[1,m]$、$\alpha\in[2^{i-1},2^i)$，点的排列$\sigma$。接下来就是ckr算法。

## Analysis of the algorithms

**lemma5.1**：分析类似于CKR+tree mertic的合体，对于每条边uv，分析它被某个点分割的概率，考虑u被它覆盖而v没有，则$K_{i-2}^{u}$里的点必然不是可能的点，所以穷举$K_{i}^{u}-K_{i-2}^{u}$中的点即可，这里面的点概率类似tree mertic的分析。

**lemma5.2**：很简单的引理，关键在于这个设置的方法，使得两个很接近的点的$A'$值大概率相似。

**近似比**：用这两个引理就可以容易的分$A'$是否相等来计算条件期望。

**去随机化**：穷举所有可能的随机变量，然后用条件期望不断的解决当前排列位置上的terminal。

