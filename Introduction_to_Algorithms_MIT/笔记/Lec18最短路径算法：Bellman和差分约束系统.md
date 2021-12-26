# Lec18 最短路径算法：Bellman和差分约束系统



## 1. Bellman-Ford algorithm

Bellman-Ford algorithm：找到所有从s到v的最短路径，或确定存在负权重循环。算法实现如下：

<img src="https://i.bmp.ovh/imgs/2021/03/715fed1bbc514bab.png" style="zoom:67%;" />



**Correctness**

Theorem：如果图中没有负权值环，通过Bellman-Ford算法之后$d[v]=\delta(s,v)$。

proof：假设$v\in V$是任何一个点，并且p是s到v的最短路径中边最少的（防止权值为0的边）。因为p是一个最短路径所有我们有$\delta(s,v_i)=\delta(s,v_{i-1})+w(v_{i-1},v_i)$。归纳证明。

<img src="https://i.bmp.ovh/imgs/2021/03/013af3acf4a79cb1.png" style="zoom:67%;" />



Corollary：如果有一个值$d[v]$在$|V|-1$次遍历后不能收敛，则证明存在负权值环。



## 2. Linear programming and  difference constraints

**Linear programming**：问题定义如下。



<img src="https://i.bmp.ovh/imgs/2021/03/9887b3267e451695.png" style="zoom:67%;" />

**Algorithms for the general problem**

* Simplex methods — practical, but worst-case  exponential time.
* Interior-point methods — polynomial time and  competes with simplex



可行性问题（Feasibility problem）：没有优化标准只需要找到满足$Ax\leq b$的可行解。通常和普通的线性规划一样困难。



**Solving a system of difference  constraints**

线性规划中A中的每一行包括一个1和一个-1，其他的都是0。可以得到如下的式子，约束可以看作是两个点之间的边。

![](https://i.bmp.ovh/imgs/2021/03/7b23cd8521143b5a.png)



定理：如果约束图包含负权重循环，那么差分系统将无法满足。

<img src="https://i.bmp.ovh/imgs/2021/03/a68fe6dd15d96257.png" style="zoom:67%;" />

定理：假设约束图中不存在负权重循环，这样约束是可以满足的。

<img src="https://i.bmp.ovh/imgs/2021/03/a523517d8f6ca517.png" style="zoom:67%;" />





<img src="https://i.bmp.ovh/imgs/2021/03/bd3643d8e4095eee.png" style="zoom:67%;" />



**Bellman-Ford and linear  programming**

Corollary：Bellman-Ford算法可以在O（mn）时间内求解n个变量的m个差分约束的系统。单源最短路径是一个简单的LP问题。

<img src="https://i.bmp.ovh/imgs/2021/03/8faf1ea6633af1fa.png" style="zoom:67%;" />



## 3. VLSI layout compaction

问题：压缩（一维）VLSI布局的要素之间的空间，而又不要使任何要素过于靠近。

<img src="C:\Users\13775\AppData\Roaming\Typora\typora-user-images\image-20210329215908807.png" alt="image-20210329215908807" style="zoom:67%;" />