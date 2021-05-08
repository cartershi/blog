---
title: "TPM_chapter4"
date: 2021-03-30T20:24:27+08:00
draft: false
tags: ["gele"]
---

# BASICS

**Chebyshev's Inequality ** $Pr[|X-\mu|\ge\lambda\sigma]\le\frac{1}{\lambda^2}$ 使用它就称为second moment method

在指示变量下，$Var[X_i]=p_i(1-p_i)\le E[X_i],~Var[X]\le E[X]+\sum_{i\ne j}Cov[X_i,X_j]]$

# NUMBER THEORY

v(n)为能整除n的素数p的个数。

**Theorem 4.2.1** 令$\omega(n)\rightarrow \infty$任意缓慢增长，使得$|v(x)-\ln\ln n|>\omega(n)\sqrt{\ln\ln n}$的$x\in\{1,...,n\}$为o(n)个。

**Proof.** 令$X_p=1$为随机选择的x可被p整除，则$E[X_p]=1/p+O(1/n)$，令$M=n^{1/10},~X=\sum X_p$(其中$p\le M$)，则$E[X]=\ln\ln{n}+O(1)$，注意对于选中的x，$|v(x)-X(x)|<10$，否则这多出来的10个的乘积大于n。分析得$Var[X]=\ln\ln{n}+O(1)$，得$Pr[|X-\ln\ln{n}|\ge\lambda\sqrt{\ln\ln n}]<\frac{1}{\lambda^2}+o(1)$。

**Theorem 4.2.2** 令$\lambda$固定，则$\lim_{n\rightarrow\infty}|\{x:1\le x\le n,v(x)\ge\ln\ln n+\lambda\sqrt{\ln\ln n}\}|=\int_\lambda^\infty \frac{1}{\sqrt{2\pi}}e^{-t^2/2}dt$

**Proof. ** 令$s(n)=o((\ln\ln n)^{1/2}),~M=n^{1/s(n)}$，同上得$V(x)-X(x)\le s(n)$。考虑理想0-1随机变量$Pr[Y_p=1]=\frac{1}{p}$，令$Y=\sum_{p\le M} Y_p$，则$E[Y]=\ln\ln n + o((\ln\ln n)^{1/2}),Var[Y]\sim \ln\ln n$。则归一化的$E[\widetilde{Y}^k]\sim E[\widetilde{N}^k]$，后面gele

# MORE BASICS

令$\Delta=\sum {Pr_{i\sim j}[A_iA_j]}$，即不独立事件发生概率之和。

令$\Delta^*=\sum {Pr_{j\sim i}[A_j|A_i]}=\Delta \sum_i Pr[A_i]=\Delta E[X]$。

**Corollary 4.3.3** if $Var[X]=o(E[X]^2)$，$X\sim E[X]$ 几乎一定

**Proof. ** 直接带入Chebyshev's Inequality，$Pr[|X-E[X]|\ge\frac{\epsilon E[X]}{\sqrt{Var[X]}}\sqrt{Var[X]}]\le\frac{Var[X]}{\epsilon^2 E[X]^2}$。

**Corollary 4.3.5** if $E[x]\rightarrow \infty,\Delta^*=o(E[X])$，$X\sim E[X]$ 几乎一定

# RANDOM GRAPHS

对于随机图G=(n,p(n))，若$p(n)\ll r(n)$则特征P几乎不满足，若$p(n)\gg r(n)$则特征P几乎满足，这个$r(n)$被称为P的临界函数。

定义$\omega(n)$为图中的最大团。

**Theorem 4.4.1** 特征$\omega(n)\ge4$的临界函数为$n^{-2/3}$

**Proof. ** 定义$X_s$为点集s为团，$E[X_s]=p^6,E[X]=\frac{n^4p^6}{24}$，若$p\ll n^{-2/3}$，则$E[X]=o(1)$，显然。若$p\gg n^{-2/3}$，由于事件对称，考虑共用两个点和三个点的情况，得$\Delta^*=O(n^2p^5)+O(np^3)=o(n^4p^6)=o(E[X])$，得结论。

**Definition 1** 定义$\rho(H)=e/v$为图H的密度，若H的每个子图$H'$密度都不超过$\rho(H)$则称H平衡，若都小于$\rho(H)$则称H严格平衡。

**Theorem 4.4.2** 令H是v个点，e条边的平衡图，事件$A(G)$是H为G的子图，A的临界函数为$p=n^{-\frac{v}{e}}$

**Proof. ** 定义为$A_S$为G的S导出子图包含H，则$p^e\le Pr[A_s]\le v!p^e$，则$E[X]={n \choose v}Pr[A_s]=\Theta(n^vp^e)$，若$p\ll n^{-\frac{v}{e}}$，则$E[X]=o(1)$，显然。反之，由于对称性，$\Delta^*=\sum_{i=2}^{v-1}O(n^{v-i}p^{e-ie/v})=\sum_{i=2}^{v-1}O((n^vp^e)^{1-\frac{i}{v}})=\sum_{i=2}^{v-1}o(n^vp^e)=o(E[X])$，由Corollary 4.3.5得结论。

**Theorem 4.4.3** 没有远大于啊，gele

**Theorem 4.4.4** 

# CLIQUE NUMBER

**Theorem 4.5.1** 令$k=k(n)\sim2\log_2n$，且${n\choose k}2^{-{k\choose 2}}\rightarrow \infty$，则有$\omega(G)\ge k$。

**Proof.**  定义$X_s$为点集s为团，则$E[X]\rightarrow \infty$，用Corollary 4.3.5。

# DISTINCT SUMS

定义正整数集$x_1,\cdots,x_k$有不同和为任意子集的和不同。令f(n)为最大的k，使得$\{x_1,\cdots,x_k\}\sub \{1,\cdots,n\}$。

显然2所有次方合法，即$f(n)\ge 1+\lfloor\log_2n\rfloor$。

**Theorem 4.6.1** $f(n)\le\log_2n+1/2\log_2\log_2n+O(1)$

**Proof.** 令$\epsilon_1,\cdots,\epsilon_k$为等概率0-1随机变量，令$X=\epsilon_1x_1,\cdots,\epsilon_kx_k$，则$\sigma\le n\sqrt{k}/2$，有Chbyshev's Inequality $Pr[|X-\mu|\ge\lambda n\sqrt{k}/2]\le Pr[|X-\mu|\ge\lambda\sigma]\le\frac{1}{\lambda^2}$，则$Pr[|X-\mu|<\lambda n\sqrt{k}/2]>1-\frac{1}{\lambda^2}$。又由于和不同，$Pr[|X-\mu|<\lambda n\sqrt{k}/2]<2^{-k}\lambda n\sqrt{k}/2$。连列即可。

# THE RÓDL NIBBLE

对于$\{1,\cdots,n\}$，定义$M(n,k,l)$为最小的k元子集的集合，其能任意的l元子集。

double counting l元子集的个数，每个k元子集最多覆盖$k\choose l$个l元子集，则$M(n,k,l)\times{k\choose l}\ge {n\choose l}$。

**Theorem 4.7.1** 对每个整数$r\ge 2$，实数$k\ge1$，$a>0$。存在$\gamma=\gamma(r,k,a)>0,d_0=d_0(r,k,a)$，使得对于每个$n\ge D\ge d_0$，n个点的r正则超图H中，若每个点度为正数，且

1. 最多$\gamma n$的点不满足$d(x)=(1\pm\gamma)D$
2. 对所有的点，$d(x)<kD$
3. 对任意的两个点x,y，$d(x,y)<\gamma D$

则H有一个点覆盖至多$(1+a)(n/r)$条边。

**Theorem 4.7.3** 对于固定的k,l，有$M(n,k,l)\ge (1+o(1)){n\choose l}/{k\choose l}$

**Proof.** 令$r={k\choose l}$，点为${n\choose l}$，边为${k\choose l}$，则$D={{n-l}\choose{k-l}},d(x,y)\le{{n-l-1}\choose{k-l-1}}=O(D)$，由Theorem 4.7.1得结论。

# Hamiltonian Paths

**Theorem 1** n个点的竞赛图，汉密尔顿路径的数目$P(n)\le cn^{3/2}\frac{n!}{2^{n-1}}$。

**Proof.** 定义$C(n)$为图中汉密尔顿回路的数目，$F(n)$为图中每个点出入度都为1的子图的数目，有$C(T)\le F(T)=per(A_T)=O(n^{3/2}\frac{(n-1)!}{2^{n}})$。考虑第n+1点与其他点等概率定向，则$E[C(n+1)]=\frac{1}{4}P(n)$，则存在一种定向，$P(n)\le 4C(n+1)le cn^{3/2}\frac{n!}{2^{n-1}}$。