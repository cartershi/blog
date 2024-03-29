---
title: "A Fast and Provable Method for Estimating Clique Counts Using Turán’s Theorem"
date: 2020-11-20T16:38:14+08:00
draft: false
tags: ["chernoff bound","sample","clique count"]
---

本文用sample的估算图中的clique数目。

## 准备

定义$C_i(H)$为图H中i-clique的集合，定义$\rho_i(H)=\frac{|C_i(H)|}{\binom{|V(H)|}{i}}$为图H中i-clique的密度。

定义$f(k)=\frac{k^{k-2}}{k!}$，则$f(k)\simeq\frac{e^k}{\sqrt{2\pi k^5}}$

Corollary 3.3 对于任意n个点的图H，若$\rho_2(H)>1-\frac{1}{k-1}$，则$\rho_k(H)\ge \frac{1}{f(K)n^2}$

直接由edros的定理即得

## clique shadows

定义clique shadows $S$为一个$\{(S_i,l_i)\}$的集合，使得$\cup_{(S,l)\in S}C_l(S)$与$C_k(H)$构成双射。

为了算法一的bound，还需要保证$\rho_l(S)\ge\gamma$，称为$S~\gamma-$saturated。

算法一本身idea很容易，sample S中的一个元素，然后sample一个l个点的tuple，$X=1$意味着这个tuple是一个clique，可得$E[X]=\frac{C_k(G)}{\sum_{s\in S}w(s)}$，这个值显然大于$\gamma$。外面套一个多次随机用chernoff bound即可。

这个算法的关键在于S需要的$\gamma-$saturated，这正是Corollary 3.3解决的东西。

## 建立saturated clique shadows

类似那个chiba-nishizeki算法，对于每个子图(S,l)，核分解之后计数不变式为$C_l(S)=\sum_{s\in S}C_{l-1}(N_s(S))$，这就保证了clique shadows。若某个子图密度够Corollary 3.3，不在处理这个子图，这就有了$\gamma-$saturated。

后面的分析很平凡了。