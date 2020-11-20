---
title: "Efficient Algorithms for Densest Subgraph Discovery"
date: 2020-11-08T10:37:29+08:00
draft: false
tags: ["Densest Subgraph"]
---

本文处理最密子图问题，它基于$(k,\Psi)-core$，可以处理普通模式，而不局限于clique。

文章用core的部分还不错。

## 问题定义

EDS为最大边密度子图，CDS为最大团密度子图，PDS为最大模式密度子图。这三者是逐渐包含关系，首先看CDS的方法，最后把它拓展到PDS（这里没意思）。

## 现有方法

### 精确算法

参见Scalable Large Near-Clique Detection in Large-Scale

### 近似算法

每次删除度最大的节点，计算剩余图密度。

##  CLIQUE-BASED CORES

### 定义

**k-core**

定义k-core $H_k$为图G中最大的子图，使得每个点的度至少为k。定义$H_k$的order为k。点v的core number定义为包含点v的$H_k$中的最大order。可以发现$H_k$中所有节点的core number至少为k。

**性质**：

1. k-cores是nested，即order更小的k-core覆盖更大的k-core。

2. k-core可以不连通。

3. 可以线性计算所有点的core number。

$(k,\Psi)$-core​

仿照k-core的定义，我们给出$(k,\Psi)$-core​ $R_k$的定义：图中的最大子图，使得每个点的clique数至少为k。定义$R_k$的order为k。点v的clique-core number $core_G(v,\Psi)$为包含点v的$R_k$中的最大order。定义最大clique-core number为$k_{max}$。

**性质**：

1. $(k,\Psi)$-core是nested，即order更小的$(k,\Psi)$-core覆盖更大的$(k,\Psi)$-core。

2. k-core可以不连通。

3. $core_G(v,\Psi)\le deg_G(v,\Psi)$

### $(k,\Psi)$-core的上下界

上界为$k_{max}$：每个点删除都会使得密度变小，所以每个点至少参与$\rho$个clique，这是$k$的定义。

下界为$\frac{k}{|V_{\Psi}|}$：double counting$R_k$中的clique涉及的点数即可。

### $(k,\Psi)$-core分解

思想在于迭代的删除图中clique数最小的节点，这个值是当前节点的$core_G(v,\Psi)$，正确性反证一下即可。

注意删除时需要更新相应节点的clique数，做法是计算有它参与的clique数并更新其他点。

### 拓展

模式可以用与$(k,\Psi)$-core分解一样的算法

## CORE-BASED APPROACHES

### 精确算法

**二分的上下界：**

借助$(k,\Psi)$-core的上下界，我们可以给出二分的上下界

上界：$(k,\Psi)$-core上界的证明没有用到$(k,\Psi)$-core的定义，可以拿过来用

下界：$\rho_{opt}\ge \max{\rho(R_k,\Psi)}\ge \frac{k_{max}}{|V_\Psi|}$

**core定位**：

这里是核心技术。

lemma7：CDS必然在$(k,\Psi)$-core中，这里$k=\lceil \rho_{opt}\rceil$

证明一句话，CDS中每个点都至少涉及$\rho_{opt}$个clique。

lemma7导致只考虑图$(\lceil \frac{k_{max}}{|V_\Psi|} \rceil,\Psi)$-core。

Pruning1：$\frac{k_{max}}{|V_\Psi|}$依然较大，进一步考虑每个$(k,\Psi)$-core的密度，选择最大密度的

Pruning2：对于Pruning1找到的core，计算它每个连通分支的密度，找最大密度

Pruning3：对于每个联通分支，binary search的gap变成连通分支的点数。~~这也能算剪枝的吗~~

**删点**：

当二分的下界变大时，可以删除一些节点。

**算法CoreExact**：

第一步计算二分的上下界，第二步定位到合适的core，第三步对每个连通分支进行计算密度。

第三步展开说一下，首先接着当前的密度对连通分支进行删点，删完后判断是否有密度更大的可能。最后进行二分算密度，过程中随着下界的变大进行删点。

### 近似算法：

**算法IncApp**：

借助二分的上下界直接有一个$\frac{1}{|V_\Psi|}$近似的算法：$(k_{max},\Psi)$-core。直接调用$(k,\Psi)$-core分解即可。

**算法CoreApp**：

用k-core的core number作为clique-core number的上界，按上界从大到小排序。每次double候选点集，对于每个候选点集，进行$(k,\Psi)$-core分解，计算$k_{max}$。由于$(k,\Psi)$-core分解复杂度与点数是线性的，double技术保证总复杂度是线性的。

### 并行化：

并行$(k,\Psi)$-core分解和最小流算法即可。

## PDS问题：

近似算法都可以直接套用，依然反证。

PExact算法跟Scalable Large Near-Clique Detection in Large-Scale一样的构造和证明。

CorePExact将同组的模式合并。