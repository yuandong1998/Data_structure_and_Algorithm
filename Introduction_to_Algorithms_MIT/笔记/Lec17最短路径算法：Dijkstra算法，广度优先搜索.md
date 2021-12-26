# Lec17 最短路径算法：Dijkstra算法，广度优先搜索 

## 1.  Properties of shortest paths

**Paths in graphs**

考虑一个带权重边的图，路径的权重为$w(p)=\sum_{i=1}^{k-1}w(v_i,v{i+1})$.

从u到v的最短路径为：$\delta(u,v)=min\{w(p:p\ is\ a\ path\ from\ u\ to \ v)\}$。

如果`u`到`v`不存在路径则$\delta(u,v)=+\infty$.

如果边的权重可以为负数，那么最短路径可能不存在，因为可能有一个负数的环。



**Optimal substructure**

Theorem: 最短路径的子路径也是最短路径。

Proof:  Cut and Paste.



**Triangle inequality**

Theorem: 对于所有的$u,v,x,\in V$，有：$\delta(u,v)\leq \delta(u,x)+\delta(x,v)$.



**Single-source shortest paths**

假设边的权重都是非负的，所有的最短路径都是存在的。

IDEA：贪心（Greedy）.

1. 维护一个从s到该集合S的点的最短路径已知的集合。

2. 每一步从$v\in V-S$中添加一个估计距离s最短点到S中。

3. 更新到v的距离。

   

## 2. Dijkstra’s algorithm

算法：

<img src="https://i.bmp.ovh/imgs/2021/03/24742d4fcf59b0a3.png" style="zoom:67%;" />

松弛操作部分可以理解为对三角不等式的约束进行不断松弛的操作，使之满足，再松弛过程中实现了降序排列Key的操作。



## 3. Correctness

**Part 1**

Lemma:初始化$d[s]=0,其他的点d[v]=+\infty$，在整个过程中对于所有$v\in V,d[v]\geq \delta(s,v)$。

proof: 反证法，假设`v`是第一个$d[v]<\delta(s,v)$的点，`u`是导致改变的点$d[v]=d[u]+w(u,v)$。所以有一下矛盾。

<img src="https://i.bmp.ovh/imgs/2021/03/d146f53ed90da685.png" style="zoom:67%;" />

**Part 2**

Lemma：`u`是`v`最短路径的前一节点，如果$d[u]=\delta(s,u)$，并且边$(u,v)$是已经松弛了的，则我们有通过松弛后$d[v]=\delta(s,v)$。

proof：松弛过程实现



**Part 3**

Lemma：Dijkstra 算法最后会计算出所有的$d[v]=\delta(s,v)$.

Proof：v 添加到S中时可以保证$d[v]=\delta(s,v)$，通过反证法证明。假设u时第一个添加到S中去$d[u]>\delta(s,u)$的。假设y是第一个u的最短路径中的S-V中的节点。当x添加时，$d[x]=\delta(s,x)$，边(x,y)是松弛过的，$d[y]=\delta(s,y)\leq\delta(s,u)<d[u]$。但是$d[u]\leq d[y]$，矛盾了。

![](https://i.bmp.ovh/imgs/2021/03/7c4193cf01f161eb.png)



## 4. Analysis

<img src="https://i.bmp.ovh/imgs/2021/03/e6b587c28a6c44c2.png" style="zoom:67%;" />



<img src="https://i.bmp.ovh/imgs/2021/03/83877cc356c79e83.png" style="zoom:67%;" />



## 5. Breadth-first search

假设对于所有的边$w(u,v)=1$ ，采用FIFO队列代替优先队列。

![](https://i.bmp.ovh/imgs/2021/03/df1d68500b8b425f.png)

