---
title: "TPM_chapter2"
date: 2021-01-03T21:24:15+08:00
draft: true
tags: ["TPM"]
---

# 定义

期望的线性性：若$X=c_1X_1+\cdots+c_nX_n$，则$E[X]=c_1E[X_1]+\cdots+c_nE[X_n]$，无论这些$X_i$是否独立。

考虑n元的重排后不动点的期望，每个位置不动的期望为$\frac{1}{n}$，由期望的线性性得总期望为$1$

考虑竞赛图哈密尔顿回路的期望，每个n元重排是回路的期望为$2^{-(n-1)}$，由期望的线性性得总期望为$n!2^{-(n-1)}$。

# SPLITTING GRAPHS

**Theorem 2.2.1** n个点m条边的图至少有m/2条边的一个二部子图。

**Proof.**  1/2的概率选点，则每条边被选的期望是1/2，期望线性性得结论。

**Theorem 2.2.2** 2n个点m条边的图至少有mn/(2n-1)条边的一个二部子图，2n+1个点m条边的图至少有m(n+1)/(2n+1)条边的一个二部子图。

**Proof.**  随机挑选n个点，依然算概率。

# 两个同色子图的结果

考虑每个$K_n$的每个a正则图，算期望，得存在一个二染色使得最多有${n\choose a }2^{1-{a\choose 2}}$个$K_a$。

考虑每个$K_{m,n}$的每个a,b正则图，算期望，得存在一个二染色使得最多有${m\choose a}{n\choose b}2^{1-ab}$个$K_{a,b}$。

**remark** 这里说的是边染色

# BALANCING VECTORS

**Theorem 2.4.1** $v_1,\cdots,v_n$为n元实数域的单位向量，则存在一个$\epsilon_1,\cdots,\epsilon_n=\pm1$，使得$|\epsilon_1v_1+\cdots+\epsilon_nv_n|\le\sqrt n$。也存在一个$\epsilon_1,\cdots,\epsilon_n=\pm1$，使得$|\epsilon_1v_1+\cdots+\epsilon_nv_n|\ge\sqrt n$。

**Proof.** 随机挑选$\epsilon_1,\cdots,\epsilon_n$，令$X=|\epsilon_1v_1+\cdots+\epsilon_nv_n|^2$，则$X=\sum_i\sum_j\epsilon_i\epsilon_jv_i\cdot v_j$。$i\ne j,E[\epsilon_i\epsilon_jv_i\cdot v_j]=0$，得$E[X]=n$

**remark** 这里的n元向量是多余条件吧？

**Theorem 2.4.2** $v_1,\cdots,v_n$为n元实数域的向量，至多是单位向量，对于任意的$p_1,\cdots,p_n\in[0,1]$，存在一个$\epsilon_1,\cdots,\epsilon_n\in\{0,1\}$，使得$|(p_1-\epsilon_1)v_1+\cdots+(p_n-\epsilon_n)v_n|\le\frac{\sqrt n}{2}$。

**Proof.** $p_i$的概率挑选$\epsilon_i=1$，如Theorem2.4.1的证明

# UNBALANCING LIGHTS

**Theorem 2.5.1** 令$\forall~1\le i,j\le n,a_{ij}=\pm1$，存在一个$x_i,y_j=\pm1$，使得$\sum_i\sum_ja_{ij}x_iy_j\ge\left(\sqrt{\frac{2}{\pi}}+o(1)\right)n^{\frac{3}{2}}$

**Proof.** 随机挑选$y_j$，定义$R_i=\sum_ja_{ij}y_j$，显然$a_{ij}y_j$是等概率$\pm1$，则$E[|R_i|]=\left(\sqrt{\frac{2}{\pi}}+o(1)\right)\sqrt n$（算概率然后斯特林公式即可），$x_i$用来调整$R_i$至绝对值，得结论。

# 构造性证明

Theorem 2.2.1：每次往割边更多的地方放。

Theorem 2.4.1：用构造法第$i$个向量加入后可控制前$i$个的l2范数$\ge \sqrt i$或$\le \sqrt i$

Theorem 2.4.2：类似上一个证明，第$i$个向量加入后，$p_i$的概率挑选$\epsilon_i=1$，数学归纳法l2范数的期望$\le\frac{\sqrt i}{2}$，所以每次挑l2范数更小的$\epsilon_i$即可。

# Brégman's Theorem

考虑n*n的01矩阵A，令$r_i=\sum_ja_{ij}$为第$i$行的1的数目，定义S为排列$\sigma$的集合，使得$\forall i,a_{i,\sigma_i}=1$，定义$per(A)=|S|$。

**Brégman's Theorem** $per(A)\le\prod_{i}(r_i!)^{\frac{1}{r_i}}$

**Proof.** 随机挑选$\sigma\in S,\tau\in S_n$，