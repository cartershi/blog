---
title: "TPM_chapter3"
date: 2021-03-29T20:59:39+08:00
draft: false
tags: ["gele"]
---

Alterations的含义是随机事件之后进行调整

# RAMSEY NUMBERS

**Theorem 3.1.1** 对于任意的整数n，$R(k,k)> n - {n\choose k} 2^{1-{k \choose 2}}$。

**Proof** 随机等概率染色，得同色的k子图数目的期望为$m={n\choose k} 2^{1-{k \choose 2}}$，必然有一个染色同色数$x\le m$，对于这个染色，从每个同色k子图中移除一个点即可。

**Theorem 3.1.3** 对于任意的整数n和$p\in [0,1]$，$R(k,l)> n - {n\choose k} p^{k \choose 2}-{n\choose l}(1-p)^{l \choose 2}$。

**Proof** p概率染蓝色。

# INDEPENDENT SETS

**Theorem 3.2.1** n个点nd/2条边的图($d\ge1$)，$\alpha(G)\ge n/2d$

**Proof** p的概率选点，点集大小期望为np，每条边在点集中的概率是nd/2$p^2$，则点数-边数的期望为$np-\frac{nd}{2}p^2$，令p为1/d，至少存在一个点集的点数-边数$\ge \frac{n}{2d}$，这个点集每条边删一个点即可。

# COMBINATORIAL GEOMETRY

S是单位正方形中n个点的集合，T(S)是包含S中三个点的最小三角形。

**Theorem 3.3.1** 存在一个S，使得$T(S)\ge \frac{1}{100n^2}$。

**Proof** 随机选三个点PQR，令$\mu(PQR)$代表围成的三角形的面积，考虑$Pr[\mu\le\epsilon]$，$Pr[b\le d(PQ)\le b+\Delta b]\le\pi(b+\Delta b)^2-\pi b^2$，点R到PQ的距离不到$2\epsilon/b$的概率至多$4\sqrt{2}\epsilon/b$，积分得$\int_0^{\sqrt{2}}(2\pi b)(4\sqrt{2}\epsilon/b)db=16\pi\epsilon$。令$\epsilon=\frac{1}{100n^2}$，则$Pr[\mu\le\epsilon]<0.6n^2$。随机取2n个点，面积小于$\frac{1}{100n^2}$的三元组期望小于n，这2n个点每个小三元组删除一个点即可。

# PACKING

不懂

# RECOLORING

m(n)见第一章的COMBINATORIOS

**做法** 1/2的概率点染红色，所有同色边涉及的点进行随机排列，若点涉及的边若依然同色，以p的概率翻转。

**证明** 设$m=2^{n-1}k$，边e先红后不变的概率易得$2^{-n}(1-p)^n$。考虑边e先不红后红的概率，不红的边变红必然是因为另一条边f先蓝，e与f只有一个公共点，所以总概率小于任意两条边满足ef的概率之和（这步是关键），对于某个固定的点排列，计算ef发生的概率即可。

# CONTINUOUS TIME

**PropertyB. ** 每个点随机一个0~1的实数作为出生时间，点按时间排序。定义T为e-v中蓝色的点，则这些点出生比v早，f-v中的点不能翻转成功，得$Pr[E_{ef}]\le \sum_{l=0}^{n-1}{n-1 \choose l}2^{1-2n}\int_0^1x^lp^{l+1}(1-xp)^{n-1}dx$。这简化了recoloring的复杂描述。

**Random Greedy Packing.** V个点N条边的k+1超图中，每个点包含在D条边中，每个点对共用$o(D)$条边。给每个点一个[0,D)的实数作为出生时间，点按时间排序，按时间将独立的边加入P，定义$P^{FINAL}=P_D$。这里由于相当于随机排序后贪心的加入点，所以算法被称为随机贪心。

证明gele