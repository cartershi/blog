---
title: "TPM_chapter1"
date: 2020-12-23T15:47:08+08:00
draft: false
tags: ["TPM"]
---

# 概率化方法

所谓概率化方法，即为了证明某些特征存在，我们定义一个概率空间，使得这些特征存在于这个概率空间且概率为正。

**例子** ramsey数$R(k,k)>\lfloor2^{\frac{k}{2}}\rfloor~\forall k\ge3$。

**证明** 定义概率空间为完全图$K_n$的随机染色，则k子图同色的概率为$2^{1-{k \choose2}}$，至少有一个同色的概率至多${n\choose k}2^{1-{k \choose2}}$。令这个值小于1，则可能给出一个无k同色子图的染色。

**remark** 考虑$K_{1024}$下的20同色子图，随机sample染色，同色的概率至多$\frac{2^{11}}{20!}$，所以随机sample很容易得到一个非同色子图。

# 图论

定义$S_k$为竞赛图中任意k个玩家都会被某一个玩家击败。

**定理1.2.1** 若${n\choose k}{(1-2^{-k})}^{n-k}<1$，则存在一个n个点的竞赛图，有特征$S_k$

**证明** 一样的证明，考虑每个k子集被击败的概率，为${(1-2^{-k})}^{n-k}$，再一个union bound即可。

**Theorem1.2.2** 若图中有n个点，最小度$\delta>1$，则存在一个至多为$n\frac{1+\ln{(\delta+1)}}{\delta+1}$个点的支配集。

**Proof** 随机p的概率选点，则被选中的点的期望为$E[X]=np$，未被这些点支配的点期望为$E[Y]\le n(1-p)^{\delta+1}$，和$E[X]+E[Y]\le np+ne^{-p(\delta+1)}$，求导即可。

**Remark1.2.2** 构造性证明：定义$C(v)$为v和v的邻居。考虑未被支配的点集r及其$\sum_{r} C(v)$，这里$C(v)$中的点都是未被挑选的，至多n个点，则至少有个点出现在$\frac{\sum_r C(v)}{n}$个r的$C(v)$中，即这些$\frac{r(\delta+1)}{n}$个点必然被支配，所以一次可以使未被支配的点减少为原本的$1-\frac{r(\delta+1)}{n}$，重复$n\frac{\ln{(\delta+1)}}{\delta+1}$次后最多剩余$\frac{n}{\delta+1}$个未被支配的点，直接全部选中得到结果。这个算法预处理$\sum C(v)$并进行后续更新，复杂度为$O(n^2)$。

**lemma1.2.3** 若图G中最小度为$\delta$且有一个小于$\delta$的割，则G的每个支配集在割的两边都有点。

**判断图是否$\frac{n}{2}$联通**：首先度数至少$\delta\ge\frac{n}{2}$，利用Remark1.2.2中的构造可得到一个$O(\log n)$的支配集，由lemma1.2.3，这个支配集必然被割拆分，所以穷举支配集并跑网络流即可。

# 组合

定义超图为n-uniform如果每条表包含n个点。称图二色可染如果存在一个点的二染色，使得每条边都不是同色的。用m(n)表示最小可能的边数，使得这个超图不是二色可染。

**Proposition 1.3.1** 对于n-uniform超图，$m(n)\ge 2^{n-1}$。

**Proof** 若边数小于$2^{n-1}$， 对于随机的二染色，一条边同色的概率为$2^{1-n}$，则图至少一条边同色的概率$<1$，所以必然有边不同色的染色。

# 组合图论

阿贝尔群G的子集A被称为sum-free若$(A+A)\cap A= \empty$

**Theorem 1.4.1** 每个n个元素非零整数的集合$B=\{b_1,b_2,\cdots,b_n\}$包含一个sum-free的子集A，$|A|>\frac{1}{3}n$

**Proof.** 定义$p=3k+2$为一个素数，且$p>2\max{\{B\}}$，$C=\{k+ 1,k + 2,\cdots,2k + 1\}$，则C是循环群$Z_p$的sum-free子群。随机选取一个$1\le x<p$，定义$d_i(x)\equiv x\cdot b_i~mod~p$，则对于固定的i，$d_i(x)$会形成$Z_p$，即$\frac{1}{3}$的概率在C中，期望是$\frac{1}{3}n$个元素在C中。这些元素在C中则不可能有sum，否则$xb_i+xb_j\equiv x(b_i+b_j)~mod~p$

**Remark.** 任意n个元素的阿贝尔群可以构造出一个$\frac{2}{7}n$大小的sum-free子集，且这个值最优。

# DISJOINT PAIRS问题

定义$\mathcal{F}$为{1,2,...,n}的m个不同子集的集簇。$d(\mathcal{F})=|\{F,F'\}:F,F'\in \mathcal{F},F\cap F'\neq \empty|$

**Theorem 1.5.1** 若$m=2^{(\frac{1}{2}+\delta)n}$，则$d(\mathcal{F})<m^{2-\delta^2/2}$

**Proof.** 反证结论。定义$A_1, A_2,..., A_t$为从$\mathcal{F}$中随机挑选的t个集合，考虑每个大小为$\frac{n}{2}$的子集，它覆盖$A_i$的概率为$\frac{2^{\frac{n}{2}}}{m}$，这样的子集最多$2^n$个，即$Pr[|A_1\cup A_2\cup\cdots\cup A_t|\le\frac{n}{2}]\le 2^n\left(\frac{2^{\frac{n}{2}}}{m}\right)^t=2^{n(1-\delta t)}$。定义$v(B)=|A\in \mathcal{F}:B\cap A=\empty|$，则$\sum v(B)=2d(\mathcal{F})\ge m^{2-\delta^2/2}$。定义Y是B中与所有$A_i$不相交的集合数目，$E[Y]=\sum{\left(\frac{v(B)}{m}\right)^t}\ge\left(\frac{\sum v(B)}{m}\right)^t\ge m^{(1-\delta^2/2)t}\ge m^{1-\delta^2t/2}$，则至少有一个$Y\ge m^{1-\delta^2t/2}$。只要令$Y\ge2^\frac{n}{2}$，又由于$Pr[|A_1\cup A_2\cup\cdots\cup A_t|\le\frac{n}{2}]>0$，则矛盾。

# The Erdós-Ko-Rado Theorem
idea：随机排序所有点，则每个排列下的连续点集被选中的概率为k/n，排序随机相当于选择的点集随机，即等于从$n\choose k$中挑选到集簇的概率。

ps: 直接double counting排列下连续序列的数目也可。