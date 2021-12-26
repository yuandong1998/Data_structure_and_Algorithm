# Lec16 贪婪算法，最小生成树



## 1. Graph representation

**Graphs**

图分为有向图和无向图，可以用$G=(V,E)$表示。

$|E|=O(V^2)$，又因为图是联通的，所以$|E|\geq|V|-1$，因此$\lg |E|=\Theta(\lg V)$.



**Adjacency-matrix  representation**

<img src="https://i.bmp.ovh/imgs/2021/03/4e68a733a02b513e.png" style="zoom:50%;" />

也可以用权重。$\Theta(V^2)$ storage，dense representation。



**Adjacency-list representation**

用表$Adj[v]$表示`v`点指向的节点。

对于无向图：$|Adj[v]|=degree(v)$.

对于有向图：$|Adj[v]|=out-degree(v)$.



Handshaking Lemma:对于无向图$\sum degree(v)=2|E|$

所以Adjacency list是一个sparse representation，$\Theta(V+E)$，经常比邻接矩阵要好。



## 2. Minimum spanning trees

输入：一个联通无向图$G=(V,E)$，和权重函数$w:E->\R$。为了简化，所有边都是互异的。

输出：一个生成树`T`，连接所有节点并且权重最小。$w(T)=\sum_{(u,v)\in T}w(u,v)$.



## 3. Optimal substructure

移去最小生成树中的任意一个边，然后T被分为了两个子树$T_1$和$T_2$.

**Theorem:** 子树$T_1$是子图$G_1$的最小生成树，子树$T_2$是子图$G_2$的最小生成树。

**Proof：** cut and paste方法：$w(T)=w(u,v)+w(T_1)+w(T_2)$.

如果$T_1'$是比$T_1$对于$G_1$更小的生成树这样$T'=\{(u,v)\}\cup T'\cup T_2$就是比$T$更小的生成树。这是与假设冲突的。



## 4. Greedy choice

**Greedy-choice property：**一个局部最优解也是全局最优解。

**Theorem：** $T$是$G$的最小生成树，$A$是$V$的子集，假设$(u,v)\in E$是$A$到$V-A$权重最小的边，那么$(u,v)\in T$.

**Proof:** 假设$(u,v)\notin T$，cut and paste.考虑T中从u到v的唯一简单路径。(u,v)和这条路径的第一个A到V-A的边交换，这样T变得更小了，假设冲突。



## 5. Prim’s greedy MST  algorithm

**IDEA:** V-A维护为一个优先队列Q，将A与V之间最小权值边的权值当作Q的key.

<img src="https://i.bmp.ovh/imgs/2021/03/693459b05e1f41f7.png" style="zoom:67%;" />



不同数据结构时间复杂度对比：

<img src="https://i.bmp.ovh/imgs/2021/03/79b2ab6be27e4594.png" style="zoom:67%;" />

如今最好算法：

- Karger, Klein, and Tarjan [1993]. 
- Randomized algorithm. 
- O(V + E) expected time