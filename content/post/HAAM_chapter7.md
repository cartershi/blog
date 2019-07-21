---
title: "HAAM_chapter7"
date: 2019-07-19T21:09:38+08:00
draft: false
tags: ["approximation algorithm"]
---

# LP Rounding and Extensions

## Nondeterministic Rounding

### Independent Rounding

集合覆盖，用LP的解作为集合被选取的概率，挑选$c\log n$次。这样期望大小有界，并且WHP覆盖所有的元素。

条件满足问题，每个元素$\frac{1}{2}$的概率为正，得到一个结果，另外以LP的解作为元素被选的概率挑选，取两者大的。

### Dependent Rounding

simultaneously rounding ：最小割问题（限制为某些点必须被割开），随机选取一个$u\in[\frac{1}{2},1]$，把比u大点与s放在一起。

Rounding against a Hyperplane：最大割问题，高级算法讲过。

Extensions：distributions on level sets、 the pipage rounding method、the level set based method、digital halftoning、cardinality constraints。~~鸽了~~

## Deterministic Rounding

Scaling：点覆盖选取所有至少$\frac{1}{2}$的点。

Filter and Round：Approximation Algorithms for Geometric Median Problems中介绍。

Iterated Rounding：上一章有。

Pipage Rounding：将小数解round成整数解，过程中保证目标函数不会增加太多。具体做法是设计一个新的目标函数，它是凸函数且与原函数近似。

Decompose and Round：几何问题可用。