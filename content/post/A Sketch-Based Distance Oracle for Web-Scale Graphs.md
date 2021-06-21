---
title: "A Sketch-Based Distance Oracle for Web-Scale Graphs"
date: 2021-05-30T16:22:10+08:00
draft: false
tags: [""]
---

本文发表于WSDM10，处理近似最短路径，结果还不错。

# 算法

**离线计算**：sample $1,2,4,\cdots,2^{\lfloor logn\rfloor}$个点的点集$S_0,S_1,\cdots$，保留每个点到这$\lfloor logn\rfloor$个点集的最近点，称为sketch。重复这个过程k次，将k个sketch融合。

**在线计算**：跟hub label一样处理。

# 近似比

考虑点ab的最短距离d，定义$A_r$为距离点a不超过$rd$的点集。注意$\frac{|A_r \cap B_r|}{|A_r \cup B_r|}$有关键的性质：$|A_r \cup B_r|\le|A_{r+1} \cap B_{r+1}|$，则若$\frac{|A_r \cap B_r|}{|A_r \cup B_r|}<1/2$恒成立，则$2|A_r \cap B_r|\le|A_{r+1} \cap B_{r+1}|$，所以成立的r不超过$\log n$。

那么对于一个不成立的r，考虑以$\frac{1}{|A_r \cup B_r|}$的概率sample点的情况，则有$\frac{1}{e}$的概率使得恰好有一个点在$A_r \cup B_r$中，又有1/2的概率在$A_r \cap B_r$中，即有常数的概率使得sample出来一个点是某个$S_i$中（这就是S集合指数递增的效果）到ab都最近且在$A_r \cap B_r$中。

进行k次sample使得这件事高概率发生。

$\Box$
