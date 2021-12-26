# Lec14 竞争性分析，自组织表

## 1. Self-organizing lists

**Self-organizing lists**

表`L`有`n`个元素，操作`ACCESS(x)`的成本为$rank_L(x)$，也就是x到头节点的长度。L可以相邻元素的交换，cost为1.



**On-line and off-line problems**

on-line：序列操作`S`,必须立刻执行操作，不知道未来的操作。

off-line：可以提前看到之后所有的操作。

Goal：最小化总成本$C_A(S)$。



**Worst-case analysis of self organizing lists**

worst case：总是访问L中的尾元素，$C_A(S)=\Omega(|S|*n)$。



**Average-case analysis of self organizing lists**

假设元素`x`以概率`p(x)`被访问，$E[C_A(S)]=\sum_{x\in L}p(x)*rank_L(x)$。其中当`L`以概率`P`降序进行排序时期望成本最小。

Heuristic:对访问的元素进行计数，然后保存`L`以计数降序排序。



## 2. Move-to-front heuristic

在实践中发现move-to-front(MTF)启发式的方法有较好的结果。具体做法是在访问`x`后，将`x`移动到表头，$cost=2*rank_L(x)$。MTF方法对于局部性方法有较好的解。



## 3. Competitive analysis of  MTF

**定义：** 一个on-line算法A是$\alpha-competitive$ 如果存在常数`k`对于任何操作序列`S`有$C_A(S)\leq \alpha*C_{OPT}(S)+k$，其中$OPT$是off-line的最优算法。



**Theorem：** MTF对于self-organizing lists是一个4-competitive。

**proof：**

首先定义一些变量：

<img src="https://i.bmp.ovh/imgs/2021/03/8d09cdd9f9cd4ce6.png" style="zoom:67%;" />



定义势能函数$\Phi:{L_i}->R$
$$
\begin{aligned}
&\Phi\left(L_{i}\right)=2 \cdot \mid\left\{(x, y): x \prec_{L_{i}} y \text { and } y \prec_{L_{i} *} x\right\}\\
&=2 \cdot \# \text { inversions }
\end{aligned}
$$
<img src="https://i.bmp.ovh/imgs/2021/03/6b13e6ead2c33c68.png" style="zoom:67%;" />

可以看出：

* $\Phi(L_i)\geq 0$ for all i>=0
* $\Phi(L_0)=0$ 如果MTF和OPT开始时一样

一次transpose，$\Delta\Phi=\pm2$，因为一次transpose会产生或者消除一个逆序对。



下面看当访问一个元素会发生什么，进行如下的定义：

<img src="https://i.bmp.ovh/imgs/2021/03/3de2caa7c0a77734.png" style="zoom:67%;" />

$r=rank_{i-1}(x)=|A|+|B|+1$，$r^*=|A|+|C|+1$.

MTF将x移动到表头，产生|A|的逆序对，消除了|B|的逆序。对OPT的每次transpose产生小于1的逆序对，因此$\Phi(L_i)-\Phi(L_{i-1}\leq2(|A|-|B|+t_i))$.



**Amortized cost**

MTF第`i`次操作的平摊代价为：
$$
\begin{aligned}
\hat{c}_{i} &=c_{i}+\Phi\left(L_{i}\right)-\Phi\left(L_{i-1}\right) \\
& \leq 2 r+2\left(|A|-|B|+t_{i}\right) \\
&=2 r+2\left(|A|-(r-1-|A|)+t_{i}\right) \\
&=2 r+4|A|-2 r+2+2 t_{i} \\
&=4|A|+2+2 t_{i} \\
& \leq 4\left(r^{*}+t_{i}\right) \\
&=4 c_{i}^{*}
\end{aligned}
$$
因此我们可以得出：
$$
\begin{aligned}
C_{\mathrm{MTF}}(S) &=\sum_{i=1}^{|S|} c_{i} \\
&=\sum_{i=1}^{|S|}\left(\hat{c}_{i}+\Phi\left(L_{i-1}\right)-\Phi\left(L_{i}\right)\right) \\
& \leq\left(\sum_{i=1}^{|S|} 4 c_{i}^{*}\right)+\Phi\left(L_{0}\right)-\Phi\left(L_{|S|}\right) \\
& \leq 4 \cdot C_{\mathrm{OPT}}(S)
\end{aligned}
$$
**Addendum**

如果将把`x`转移到表头的代价看作0（x从表中拆除在插在表头，时间是常量），则MTF是2-competitive。



如果$L_0\neq L_0^*$

* $\Phi(L_0)$最差情况为$\Theta(n^2)$。
* 因此：$C_{MTF}\leq 4*C_{OPT}(S)+\Theta(n^2)$，也是4-competitive，因为$|S|->+\infty$，$n^2$也是常量，n不受到|S|的影响。