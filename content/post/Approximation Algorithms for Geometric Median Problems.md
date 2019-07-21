---
title: "Approximation Algorithms for Geometric Median Problems"
date: 2019-07-20T16:32:30+08:00
draft: false
tags: ["论文学习","gele"]
---

作者：Jyh-Han Lin、Jeffrey Scott Vitter

个人觉得它的引理6写错了。

这篇文章的算法容易理解，就是用LP的解算每个点距离的期望$\widehat{C_i}$，定义i的邻居为$\le(1+1/\epsilon)\widehat{C_i}$的所有点，定义i的拓展邻居为两跳之内的邻居。按$\widehat{C_i}$递增排序后不断挑选点并删除x的所有拓展邻居，这些拓展邻居都用x当作中心计算距离。

可以发现1.拓展邻居是对称的，2.挑选的点的邻居不相交，3.（我感觉不需要它也行啊），4.每个点被拓展邻居覆盖时，此时的期望距离最多为它本身的期望距离，5.每个点j到它对应的中心距离$\le2(1+1/\epsilon)\widehat{C_j}$，6.反证可得每个点邻居的y的和$>\frac{1}{1+\epsilon}$（这步是关键，注意我看的那版论文里应该写反了）。

5直接说明距离的近似（LP式第一条约束）。接下来考虑中心个数，最优解是y的和，由于挑选的邻居不相交，对于每个挑选的点，由6得它的邻居y的和至少为$>\frac{1}{1+\epsilon}$，得这些邻居y的和$>\frac{1}{1+\epsilon}U$，于是得$s>\frac{1}{1+\epsilon}U$，即可。

接下来欧式距离那玩意鸽了