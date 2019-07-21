---
title: "An improved approximation algorithm for the 0-extension problem"
date: 2019-07-21T14:24:25+08:00
draft: true
tags: ["论文学习"]
---

作者：Jittat Fakcharoenphol, Chris Harrelson, Satish Rao, Kunal Talwar

## Introduction

这篇文章有一个漂亮的relaxation，它relax出一个新的semimetric度量，只保证terminal之间的距离不变即可。

## Notation

定义$A_u$为u最近的terminal或者到它的距离。显然每个点挑选$A_u$是不合理的，因为terminal之间的距离可能是$O(A_u)$级别的，若$d(u,v)$很小，则显然无法很好的近似。

## The CKR algorithm

随机一个terminal的序列，选择一个$[1,2)$的数$\alpha$，每个点u赋值给序列中第一个距离小于$\alpha A_u$的的点。

对于目标函数的两点距离，$\delta(f(u),f(v))\le\delta(f(u),u)+\delta(u,v)+\delta(f(v),v)$直接可以解决前两种情况。