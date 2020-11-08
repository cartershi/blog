---
title: "Scalable Large Near-Clique Detection in Large-Scale Networks via Sampling"
date: 2020-10-07T16:27:23+08:00
draft: false
---

本文处理最密clique子图问题。为了方便描述，下文只考虑常规图，不考虑二部图。

## Notation

定义$C_k(G)$为图G中的k-cliques集合，$c_k(G)=c_k=|C_k(G)|$为k-cliques的数目，$f_k(v)$为点v参与的k-cliques的数目，则我们有

$\sum_{v\in V(G)}f_k(v)=kc_k$

## Exact Algorithms

### 方法A

使用网络流定义，定义A为图中的点集， B为$C_{k-1}(G)$。建图方式如下：

1.s到A中的点v建立容量为$f_k(v)$的有向边。2.A中点若能与B中团构成k-clique，则建立容量为1的有向边。3.B中团到A中对应节点建立容量为无限大的有向边。4.A中的点到t建立容量为kD的有向边。

考虑上面网络的最小割，s到其他点的割为$kc_k$，这是割的上界。

定义$A_1=S\cap A,B_1=S\cap B,A_2=T\cap A,B_2=T\cap B$，显然$B_1$对应的点都在$A_1$中，计算124三种割的贡献，第一种为$\sum_{v\in V(A_2)}f_k(v)$，第4种$kD|A_1|$。

用$c_{k}^{(j)}$定义为k-clique中有j个节点在$A_1$中，对于$j=1,\cdots,k-1$，每个在$A_1$中的节点对应的k-1-clique至少有一个节点不在$A_1$中，所以它不在$B_1$中，所以必然对第二种割有1的贡献。

综上，总的割为$\sum_{v\in V(A_2)}f_k(v)+kD|A_1|+\sum_{j=1}^{k-1}jc_k^{(j)}$。

注意到$\sum_{j=1}^{k}jc_k^{(j)}=\sum_{v\in V(A_1)}f_k(v)$，带入上式得$kc_k+kD|A_1|-kc_k^{(k)}$，那么点集|A_1|不为空就能得到一个密度大于D的子图。

由于稀疏图上clique数目较少，列举速度比较快，所以本算法跑的比较快。

### 方法B

这个方法就比较简单，论文里写的有些问题。这里A为k-clique，B为所有点，s往A的容量设为1，A往B的容量设为无限，B往t的容量设为D。

这样$A_1$中所有的k-clique对应点必然在|B_1|中，并且若在$B_1$中的点不对应$A_1$任何clique，则可以放入$B_2$得到更小的割。割为$c_k-|A_1|+n|B_1|$。

## Densest Subgraph Sparsifiers

超图的点为原图中的点，边为原图中的k-clique。对这个图上的超边进行sample。

定理4本身比较难构造，关键在于这里的logn。对于任意密度$\ge D$的点集，sample后的密度高概率$\ge (1-\epsilon)C\log{n}$，任意密度$\ge D$的点集，sample后的密度高概率$< (1-\epsilon)C\log{n}$。

不过感觉sample需要D很大判断，没有实际意义

其证明本身比较简单，直接对每个点集的结果进行Chernoff bound求和即可。

