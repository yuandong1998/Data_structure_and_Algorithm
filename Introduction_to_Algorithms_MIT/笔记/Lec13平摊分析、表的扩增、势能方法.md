# Lec13 平摊分析，表的扩增，势能方法

平摊分析（Amortized Analysis）

## 1. Dynamic tables

一个哈希表多大合适？我们知道越大搜索时间越小，但越大浪费空间越多。比较好的大小为$\Theta(n)$。但如果n是未知的呢？这时可以用动态表解决，动态表的思想是当表溢出时，增大表的大小，就像malloc或new申请一个新的表，然后将旧表的项移动到新表。

**Worst-case analysis**

考虑一个有n个插入操作的序列，在最坏情况下的时间为$n*\Theta(n)=\Theta(n^2)$，**WRONG!**，因为不是所有操作都是最坏情况。

定义一个$c_i$代表第`i`次插入的代价，$=\left\{\begin{array}{ll}
i & \text { if } i-1 \text { is an exact power of } 2 \\
1 & \text { otherwise }
\end{array}\right.$，表每次扩2倍大。在2的power时进行扩大，代价为`i`。其他情况下cost为`1`。
$$
\begin{aligned}
\text { Cost of } n \text { insertions } &=\sum_{i=1}^{n} c_{i} \\
& \leq n+\sum_{j=0}^{\lfloor\lg (n-1)\rfloor} 2^{j} \\
& \leq 3 n \\
&=\Theta(n)
\end{aligned}
$$
因此，dynamic-table操作的平均时间为$\Theta(n)/n=\Theta(1)$.

**Amortized analysis**

这种分析方法即为平摊分析（Amortized Analysis），用于分析序列操作，然后分摊到每个操作去。没有用的概率，平摊分析可确保在最坏的情况下每个操作的平均性能。

**Types of amortized analyses**

有三种方法：

* the aggregate method，

* the accounting method,
* the potential method

## 2. Aggregate method

刚刚介绍的是the aggregate method，比较简单。但是其他两种方法允许将特定的摊销成本分配给每个操作。

## 3. Accounting method

对第`i`个操作收取一个费用$\hat c_i$，一个元操作收取一元，执行此操作将消耗此费用。任何未立即消耗的金额都存储在银行中，以供后续操作使用。银行余额不得为负！我们必须确保对于所有的n:$\sum_{i=1}^{n} c_{i} \leq \sum_{i=1}^{n} \hat{c}_{i}$.因此，总摊销成本为总真实成本提供了一个上限。



**例子**

对$\hat c_i=\$3$，1个用来支付插入操作，2个用来存入银行。当表扩大的时候，1个钱用来移动一个项。

银行余额永远不会低于0。因此，摊销成本的总和为真实成本的总和提供了一个上限。

<img src="https://i.bmp.ovh/imgs/2021/03/b6357b14e88b4ae0.png" style="zoom:50%;" />



## 4. Potential method

**IDEA：** 将银行帐户视为动态集的势能（按物理原理）

**Framework:**

1. 从初始数据结构$D_0$开始

2. 操作`i`将$D_{i-1}$转化为$D_i$.

3. 操作`i`的cost为$c_i$.

4. 定义势能函数$\Phi :{D_i}->R,\Phi(D_0)=0 ,\Phi(D_i)>=0$,

5. 平摊代价  $\hat c_i=c_i+\Phi(D_i)-\Phi(D_{i-1})$

   

<img src="https://i.bmp.ovh/imgs/2021/03/7c5c42c3c849922d.png" style="zoom:67%;" />

n个操作的总平摊成本：$\sum_{i=1}^{n} \hat{c}_{i}=\sum_{i=1}^{n}\left(c_{i}+\Phi\left(D_{i}\right)-\Phi\left(D_{i-1}\right)\right)=\sum_{i=1}^{n}c_i+\Phi(D_n)-\Phi(D_0)\geq \sum_{i=1}^{n} c_i$



**Potential analysis of table  doubling**

第`i`次插入后的势能，定义$\Phi(D_i)=2i-2^{\lceil \lg i \rceil}$，假设$2^{\lceil \lg i \rceil}=0$

<img src="https://i.bmp.ovh/imgs/2021/03/0be4cc3450eebf77.png" style="zoom: 67%;" />

![](https://i.bmp.ovh/imgs/2021/03/6168d499c3f1b09f.png)



![](https://i.bmp.ovh/imgs/2021/03/1c09e78db4040c56.png)



## 5. 小结

- 摊销成本可以提供数据结构性能的清晰抽象。
- 当需要进行摊销分析时，可以使用任何一种分析方法，但是每种方法在某些情况下都可以说是最简单或最精确的。
- 在accounting方法中分配摊余成本的方法可能不同，在potential方法中分配潜力的方法也可能不同，有时会产生根本不同的界限。