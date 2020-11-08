---
title: "Making Data Structures Persistent"
date: 2020-09-21T12:35:15+08:00
draft: true
---

本文提出一种将数据结构持久化的通用方法。它适用于特定的数据结构linked data structure，即

- 包含有限个点
- 每个点包含的域有限（包含数据域和指针域）
- 数据结构的访问使用有限个entry nodes

## PARTIAL PERSISTENCE

### The Fat Node Method

将域扩充为无限大，每次修改将修改的值放入额外的域中。问题在于fat node保留了所有的m次更新，需要$O(\log m)$的时间来查找某个版本的数据。这里的做法是原数据结构中的每个域按版本号建立一个查找树。

### The Node-Copying Method

为了解决fat node增加过大导致查找变慢的问题，node copy限制了域的数目。当域的数目超过某个固定值，则创建新的节点，只保留最新的结果。当然所有指向这个节点的先驱都需要更新指针域，这是个递归的过程。

为了保证递归后的均摊时间复杂度依然$O(1)$是，需要添加一个新的限制

- 每个点被引用的次数上限是常数

定义d为指针域的上界，p为前驱指针的上界，e为额外域的上界。为了简化描述，这里数据域更新直接进行复制，指针域更新放入额外域中。定义S为因为满了被复制的节点的集合。更新操作分为两步，第一步处理更新和反向指针，并将被复制的节点存入S中；第二步将S中的节点全部更新。

#### 空间复杂度分析

定义势能函数为$\frac{e}{e-p+1}*\#live\_nodes-\frac{e}{e-p+1}\#unused\_extra\_fields$，则初始值为0且始终非负。第一步的均摊空间复杂度显然是$O(1)$，因为势能的变化被更新次数t直接bound住了。对于第二步，定义均摊空间复杂度为创建的节点数+势能的增加量，设新建的节点数为k（这种复制不会增加live的），被使用的域最多为$p(t+k)-k$个，而新建节点增加的域为$ke$个，所以得均摊空间为$k+(p(t+k)-k-ke)*\frac{1}{e-p+1}=\frac{pt}{e-p+1}$，显然是$O(t)$的空间。

时间复杂度可以在上面的势能函数上乘以一个新建节点的倍率用上面一样的分析。

## FULL PERSISTENCE

### The Version Tree and the Version List

![image-20200922161831008](..\..\static\pic\6.851\full_persistence_version_list.png)

这张图简明的说出了version tree和versionlist的构建，重点在于新建版本成为version tree中父版本的第一个儿子，那么在version list里就是紧挨着父亲的节点。

### The Fat Node Method

这里与之前的不同在于需要考虑中间版本修改对于后面的影响。设修改f域的第$i$个版本，首先查找f最接近的上一次被修改的版本$i_1$和下一次被修改的版本$i_2$，以及i的后续版本$i+$。若$i_1=i$，那么直接替换。若