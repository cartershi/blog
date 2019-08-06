---
title: "A POLYNOMIAL-TIME APPROXIMATION SCHEME FOR MINIMUM ROUTING COST SPANNING TREES"
date: 2019-07-26T21:13:20+08:00
draft: false
tags: ["论文学习"]
---

作者：BANG YE WU, GIUSEPPE LANCIA, VINEET BAFNA, KUN-MAO CHAO, R. RAVI k,
AND CHUAN YI TANG

HAAM 59章的相关内容。

目标是找一棵联通树，使得$\sum_{u,v\in V}\lambda(u,v)d_T(u,v)$最小，下面称为cost，树T的cost写为c(T)。

## An application to computational biology

**A reduction from the general to the metric case**：思想就是在metric closure上找树T，可以$O(n^3)$在原图上找到一棵树Y，Y的cost不会大于T的cost。算法正确性的证明很容易，难的是算法的设计：不断找T上一条非图边ab（即一条路），将其进行删除，连接b到a-b的最短路的第二个点x，这样还可能变大，可能需要替换T上x的父亲y到x的路为a到x。（值得借鉴的想法）

## A PTAS for the ∆MRCT problem

$P^a=|VB(T,P,i)|,P^b=|VB(T,P,j)|$分别定义为i，j的最短路P切开T后与i，j连接的点数，$P^c$是树中剩下的点。

minimal δ-separator定义不提了。它的直观感受是树中很多点到根的路都需要经过一个连通分支。

k-star定义为非叶子节点最多k个的生成树，minimum k-star T定义为C(T)最小的k-star。

$\delta$-path定义为生成树上路径P，满足$P^c\le\delta n/2$。$\delta$-spine定义为树T的minimal δ-separator的边划分，使得每条路径都是$\delta$-path。

$\delta$-spine的构造是在minimal δ-separator上把所有的分支节点给断开，若叶子为h个，则会得到最多2h-2个端点，接着将这些非$\delta$-path的路径给拆开。考虑总的路径被拆开的次数，总的$P^c\le n-h\delta n$，可得拆开次数的上界，每次拆开点数加一，于是可得Lemma 5.9。

Lemma 5.12给出了任意树T的cost与它的$\delta$-spine的关系。证明就是将点的距离换成边被计算的次数，然后将边分为separator和非separator的，separator上的边借助$P^a,P^b,P^c$的定义换算即可。

Lemma 5.13直接给出了近似比的保证，思路是借助lemma 5.9得到一定可以在最优的树上得到$\lceil2/\delta\rceil-3$个点，它们在树上的路形成了$\delta$-spine，将这些路直接连边，其他的点都直接接到原来separator上的端点，$P^c$中的点统一直接连接到path中的某一个点。这样一定是一个$\lceil2/\delta\rceil-3$-star，称它为X，这个X是可以通过穷举star和所有端点得到的。

计算C(X)：分成spine和非spine的边，spine上的边用spine的定义转化，非spine上的边将它接的点分成原来直接接在separator的端点上和原来接在path上的，接在path上的用三角不等式转化为在separator上的距离和separator到端点的距离，这步很麻烦但是思路很容易，这样得到C(X)的上界。接下来用加权平均数替换min，可得这个X与最优结果的近似比。~~神一般的证明~~

这样就得到了∆MRCT的ptas

## Finding the best k-star

### A polynomial-time method

一个简单的办法是穷举k个点和它的结构，然后穷举每个点下面挂的点的个数（注意X的定义决定了这些点宫n-k个并且直接挂在k个点下面），这些点具体是什么对X的影响只有自己到其他点的距离，所以这是一个匹配问题，$O(n^3)$​可解。

## A faster method

思路就是将穷举的顺序进行控制，使得相同k-star下挂载点的个数的相邻排列满足关系$\sim$，这个可用递归得到：递归(k,n-k)的排列，使得第一个字典序最小，最后一个字典序最大。第一位为0，后面是(k-1,n-k)，递归可得；接着第一位为1，后面为(n-k-1,0,...0)，与前一个只差前两位，为(k-1,n-k-1)字典序最大的，是(k-1,n-k-1)的倒序，递归可得。最终第一位n-k-1，后面只有一个1，直接将第一位变成n-k，后面清零即可。相差的两点直接找他们之间最短的增广路。

## Optimal communication spanning trees

这个结论太老了，直接用那个$O(\log n)$的tree metric可以做到$O(\log n)$的近似比。