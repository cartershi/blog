---
title: "Mit6.851_L01"
date: 2020-09-08T15:47:13+08:00
draft: true
tags: ["data structure"]
---

本节课的主题是persistent data structure

## 持久化数据结构分为以下四种

Partial Persistence：可以查询任意版本，但只能在最新版本上做更新

Full Persistence：读写任意版本

Confluent Persistence：读写任意版本，将多个版本进行组合产生新版本

Functional Persistence：数据不可变，改变都是产生新版本

## Partial persistence

构造：用日志记录修改，当日志足够多时，创建新节点。新节点只保留最新的结果，将所有指向老节点的节点的指针使用日志进行更新（这里使用日志更新指针查找时可以按版本号找指针，不过缺点是要更新的节点比较多。），将所有老节点指向的节点的反向节点直接更新（反向节点是持久话额外需要的）。

时间复杂度：考虑均摊复杂度，用节点中的日志数作为势函数

## Full persistence

首先处理版本表示，这里使用版本树的in order顺序，记录进入和离开的时刻。为了$O(1)$判断孩子和插入，需要一个数据结构TBD。实现来说，判断孩子意味着顺序上都包含，v作为w的孩子意味着在bw之后添加bv，ew之前添加ev（为什么不是一起插在bw之后？）

时间复杂度：考虑均摊复杂度，用节点中的空位数作为势函数

这文章写的太简略了，参考[这里](./Making Data Structures Persistent.md)

## Confluent persistence