---
title: "Chapter20"
date: 2019-07-03T13:24:42+08:00
draft: true
tags: ["data structure","quadtree","octree","gele"]
---

# Quadtrees and Octrees

quadtree本意是将一个二维区域用平行于坐标轴的两条线将其分为4个区域作为树的4个孩子，因此称为quad tree。在3维空间，则有$2^3=8$个孩子，这叫做octree。更高维度的被称为hyperoctrees。通常情况下quadtree，octree，hyperoctree都叫quadtree。kd-tree与quadtree的不同在于kd-tree每层只选择某一维作为拆分的标准，所以只有两个孩子。竟然有专门的书介绍quadtree的相关内容，可见它多么复杂。

## Point Data

### Point Quadtree

多维点是最简单的情况，通常对于它有这样几种查询：1.区间查询，19章range tree处理的问题。2.球型区域查询，给定点和半径，查这个球里面的区域。3.查找每个点的最近邻。当然查找、插入、删除这些基本操作也是要支持的。

考虑二维情况，point quadtree就是在当前区域选一个点作为根，用它将区域分成四部分，每部分是一颗子树（如果按x轴分成两个区域，就是一颗BST）。

![fig20-1](/pic/data structure/20-1.jpg)

**建立**：将n个点直接排序，取中间节点，$O(n)$时间将其分成4个子区间，这样保证每个子区间不会超过n，用数学归纳法得建立时间为$O(n\log n)$。

**查询**：类似BST的查找，不过要比较两维。

**插入**：先查找到叶子，然后在叶子下面挂1层高树。

**删除**：很麻烦，书上没写。

在d维情况下将会导致每个点有$2^d$个孩子，kd-tree可以处理这个问题，因为它轮流的选取d维作为每一次层的标准，这样就相当于编码了$2^d$个孩子，可以在不平衡的地方进行处理，完全不处理的kd-tree等价于一棵quadtree。接下来只关注 region quadtree，即平分区间长度而非平分所有点。这样不能向point quadtree保证产生一棵平衡树，但是作者喜欢。

### Region Quadtree

定义cell类似于树中node，subcell相当于后代，supersell为祖先，immediate描述父子关系。空间分析非常显然，point quadtree提到四个操作都很容易处理，注意插入时需要不断地细分空间直至两点被分开，删除可以需要不断的往根删直至有至少两个孩子。

### Compressed Quadtrees and Octrees

Quadtree 鸽了

## Spatial Queries with Region Quadtrees

### Range Query