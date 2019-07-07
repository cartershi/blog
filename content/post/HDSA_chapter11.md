---
title: "Chapter11"
date: 2019-07-02T19:08:12+08:00
draft: true
tags: ["data structure","BST","AVL tree","gele"]
---

# Balanced binary search trees 

直接跳到11.3节了，平衡树平衡策略分为三种：子树高度的限制，子树大小的限制，多路搜索树的二进制化。

重新平衡的思路基本上都是从叶子开始往根修复平衡，修复的方法是rotation，它将一个子树的高度减1，另一个加1。大多数的算法逆着路径上执行一次单旋或双旋。另外一种重新平衡的思路是重建某一颗子树。

有一些BST的重平衡时间低于log，这在一些场合比较有效，例如计算几何中有些情况下rotation复杂度不是O(1)。以及并发的重平衡。

## AVL Tree

AVL树是1962年发明的远古数据结构，它基于子树的高度进行平衡，采用rotation重平衡。AVL树要求对于任意点，它的子树高度差最多为1。直接对高度做induction，可得高度为h的AVL树至少有$F\_{h+2}-1$个点，即深度是$O(\log n)$。重平衡是逆着路径进行单旋，或者双旋，或者调整子树信息。插入时最多进行一次旋转。在AVL树中如果只插入或者只删除，那么均摊时间是$O(1)$，否则是$O(\log n)$。

## Weight-balanced tree

Weight-balanced树基于子树的weight进行平衡，weight定义为叶子节点数。它要求每个点的weight与它右孩子的weight的比值在$[\alpha,1-\alpha]$之间。每上升一层，weight至少为原来的$\frac{1}{1-\alpha}$，这样得到深度和weight之间的关系。重平衡也是单旋或双旋，不同的是重平衡完成后再次重平衡至少需要当前weight的常数倍次的更新，这就导致了所谓的均摊时间少于$O(\log n)$。

## Balanced Binary Trees Based on Multi-Way Trees

binary B-trees类似trie的二进制实现那样，把一个节点拆成多个节点实现成二叉树。Symmetric Binary Trees或者通常被称为红黑树是2,3,4树的二进制实现。AA trees与红黑树等价，但是实现起来很容易。~~完全不讲细节的~~

看到11.5