---
title: "Efficiently computing k-edge connected components via graph decomposition"
date: 2020-12-27T17:06:33+08:00
draft: false
---

本文处理k联通分支算法。

论文比较简单，稍微写写

# 算法

改造经典的stoer-wagner算法，在一轮mas后处理最后的两个点s与t，若它们是k联通，则合并，否则删边。

# 优化

主要有4个优化

## 斐波那契堆

mas需要用斐波那契堆，这里是无权图，所以直接每个权值开一个链表数组，用po记录最大权值，extract-max时探查最大值，update时顺序更新po。时间复杂度考虑最大值变化的次数即可。

## 早期合并

注意到mas过程中找到的所有不小于k必然是超越的k联通，所以直接缩点。

## 早期分离

mas列表中倒序的连续小于k可直接分裂

## 提前删点

度不到k的点可直接删除

