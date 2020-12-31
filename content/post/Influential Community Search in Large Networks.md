---
title: "Influential Community Search in Large Networks"
date: 2020-12-27T18:50:17+08:00
draft: false
tags: ["cohesive"]
---

没啥意思的论文

# 问题定义

f(G)定义为图G中点的最小权值

k-influential community $H^k$定义为满足以下条件的G的导出子图
1. Connectivity: 联通
2. Cohesiveness: 每个点的度至少为k
3. Maximal structure: 不存在另一个导出子图H使得(1)H connectivity且cohesiveness, (2)H 包含$H^k$, (3) f(H) = f($H^k$)

问题是找top-r最大f值的k-influential community。

这个问题的定义会有冗余，定义non-contained k-influential community为满足以下性质的k-influential community

4. Non-containment: $H^k$不包含一个子图$\overline{H}^k$，使得$f(\overline{H}^k)>f(H^k)$

问题是找top-r最大f值的non-contained k-influential community。

# 在线做法

Algorithm2: 对于k-core，删除权值最小的点，然后DFS删点保证Cohesiveness，倒序输出即可。

对于non-contained k-influential community问题，删除点后需要图为空，否则不是non-contained k-influential community。

# 索引

注意到在线做法实际上形成了一棵树，所以只需要在每个节点保留它这一轮删除的节点即可。

注意到每个点出现k树的前提是度数至少为k，所以度数为d的点最多出现在前d棵树中，这就导致树节点的空间复杂度为$O(m)$。

个人没感觉它的算法5好在哪儿，把算法3的第3行放在外面不就行了...

# 动态图

定义太麻烦，gele