---
title: "Efficient Algorithms for Densest Subgraph Discovery on Large Directed Graphs"
date: 2020-11-25T16:53:15+08:00
draft: false
tags: ["Densest Subgraph"]
---

 本文有向图找出两个点集S和T使得密度最大（边只计算S到T的）

$\rho=\frac{E(S,T)}{\sqrt{S}\cdot\sqrt{T}}$

## 现有算法

精确算法来自ICALP09的On Finding Dense Subgraphs。里面的2近似算法不对，精确算法

### 精确算法

点集复制两遍，称为A和B。从s到A中每个点边权为m，从A到t边权为$m+\frac{g}{\sqrt{a}}$，从s到B中每个点边权为m，从B到t边权为$m+\sqrt{a}g-2d_{G}^{+}(u)$，，B到A在图G中的边对应边权为2。这里的a是一定会被穷举到的$|\frac{S}{T}|$。

证明比较有意思，直接最小割一算完运用被穷举到的$|\frac{S}{T}|$即可得一个更小的割。另外如果有一个密度更小的子图，带入割的公式可得永远不可能变成更小的割。（漂亮的构造和证明）

## 近似算法

依然穷举$|\frac{S}{T}|$，然后线性去计算。

## 新精确算法

又来定义core了：[x,y]-core为S中点出度至少为x，T中点入度至少为y。那么[x,y]-core是nested的，还有经典的lemma5.5（这个core分解的核心），这里看起来复杂的值不过是$\frac{E}{2S}$与$\frac{E}{2T}$。这个结论导出了Theorem 5.6。

### Core-Exact

Theorem 5.6导出了Core-Exact：用目前知道的近似比作为下界，二近似结果的2倍作为上界，二分密度即可，注意这里l保证一定是合法的密度。

### DC-Exact

用ICALP的结论，漂亮的分治加速。关键点在于ICALP的结论得到的关于g的公式的分母是关于$a^2$的反比例函数，导致[b,c]区间可以直接跳过。

需要注意的DC-Exact的第6行

## 新近似算法

经典的最大[x,y]-core有近似比，这里最大的定义是xy最大，易得2近似。关键在于发现[x,y]-core的$xy\le m$，，所以穷举x到$\sqrt{m}$算y，然后穷举y到$\sqrt{m}$算x即可。