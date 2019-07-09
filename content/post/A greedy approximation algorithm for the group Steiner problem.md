---
title: "A greedy approximation algorithm for the group Steiner problem"
date: 2019-07-08T09:39:22+08:00
draft: false
tags: ["论文学习"]
---
作者 Chandra Chekuri, Guy Even, Guy Kortsarz

## 2. Preliminaries

本文处理的是group steiner tree problem restricted to trees，输入为一个**有根的非负权有向树T**以及m个点集$g_i$，树T'被称为z-cover表示它至少了与z个点集相交，目标是找到一个权重最小的z-cover树。记$n=|\cup_{i=1}^{m}g_i|,s=\sum_{i=1}^{m}|g_i|$，点集$g_i$中的点都称为terminal（终端）。

虽然这里处理的图是树，但是A tight bound on approximating arbitrary metrics by tree metrics(STOC'03)证明了用树可以$O(\log n)$近似图中两点距离，所以可以直接用那个近似图之后用本文对得到的树来近似。

**预处理**：注意到非终端的叶子可以直接删除，树中度为2的非终端节点也可删除，再用一个集合包含树中所有的点，这样新树的点数是$O(n)$，且每个点都是终端，最后scale边权使得所有的正边权都大于等于1。

$\alpha-faithful$树的定义看起来就是为了claim2.3准备的。

## 3. A recursive greedy algorithm with geometric search

引用的算法，思路在HAAM5里面有过介绍（算法不同，证明的思路类似），就是对于一棵树，首先使用height reduction将其高度减少为$O(\frac{\log n}{\log\log n})$，这会导致结果近似，然后用degree reduction将每个点的度减少为$O(\log n)$，这样是精确的。在这棵树上做类似集合覆盖的算法，近似比直接套用那里的引理。

Geometric search主要的不同在于不穷举所有的子集，而是取幂次，这招height reduction也用了，不过这里不从零开始。

lemma3.3证明用了geometric之后就可以把时间复杂度减少到n的多项式，与树高无关，它的证明思路也就是bound调用子函数的次数，每一轮的调用次数容易bound，循环的轮数要注意子函数最少返回覆盖z''/h个终端的树，z''又有下届，所以可以bound。

lemma3.4的证明和引用的那个很像，不同在于两点：1.有一些重要的点和不重要的点，不重要的点由于geometric不会被调用，直接近似掉。2.考虑重要的点中密度最小的子树，它对应的参数由于geometric不一定调用，但是调用最靠近它的参数的那次与它之间密度的关系。剩下的证明就一样了。

## 4. Height reducing transformation

这玩意不是一个HAAM第5章里面的height reduction的，那里处理的是完全图，这里处理的是树。

$\alpha-decomposition$就是对$T_r$dfs，遇到轻节点回溯，这样访问到的所有节点。skeleton是$\alpha-decomposition$中的$T_r$的重节点形成的子树。branch定义我看了好久，它误导人的地方在于maximal subpath，其实就是从不止一个孩子的节点往下走，直至碰到一个多孩子的节点，这就是一个branch。（个人觉得它这里的branch包含了skeleton的叶子到分支节点的路径，不然没有$2\alpha-1$个branches吧）搞懂这个定义，算法就很容易理解了，首先得到$\alpha-decomposition$，对它的skeleton进行dfs计算所有的branch，计算所有branch的bunch，用3层高的路近似根到它的路径。

高度直接递归计算。近似比的证明思路在于原树的$\alpha-decomposition$和reduce完的那个三层的树一一对应，考虑每个$\alpha-decomposition$的每个branch到根的联通树$Q[S_B]$，它与对应的$Q'[S_B']$可用bunch证明近似，在由于branch两两不相交且个数为$O(\alpha)$，所以$\sum Q'$可用$O(\alpha)Q$bound~~这其实也可以直接分析每个branch，而不带根，然后bound边被重算的次数，就是HAAM5章那个思路~~。

## 5. Degree reducing transformation

这个算法就是将树转化成一颗每个点度最多$\beta$的树，使得树的高度不会增加超过$\log_{\beta/2}n$。这个结论感觉挺有用的。

算法就是将小的节点合并。用一个点拼接它。