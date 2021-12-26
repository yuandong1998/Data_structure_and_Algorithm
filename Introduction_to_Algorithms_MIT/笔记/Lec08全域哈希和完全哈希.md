# Lec08 全域哈希和完全哈希



## 1. A weakness of hashing

Problem: For any hash function h, a set of keys exists that can cause the average access time of a hash table to skyrocket.存在一组keys插入同一个slot，影响速度。

IDEA：random

## 2. Universal hashing 全域哈希

**定义：** Let $U$ be a universe of keys, and let $H$ be a finite collection of hash functions, each mapping $U$ to $\{0, 1, …, m–1\}$. We say H is universal if for all $x, y ∈ U$, where $x ≠ y$, we have $|{h ∈ H : h (x) = h (y)}| = | H|/ m$. 

随机的从H中选取h，x和y发生collision的概率是1/m.



## 3. Universality theorem 

**Theorem:** Let h be a hash function chosen (uniformly) at random from a universal set H of hash functions. Suppose h is used to hash `n` arbitrary keys into the `m` slots of a table T. Then, for a given key x, we have$E[\#collisions  with x]<n/m$. 其中 $n/m$：load factor. 

为什么是小于？



**Proof**

Let $C_x$ be the random variable denoting the **total number** of collisions of keys in T with x and let $c_{x y}=\left\{\begin{array}{ll}
1 & \text { if } h(x)=h(y) \\
0 & \text { otherwise. }
\end{array}\right.$ ，$C_x$表示和$x$碰撞的key的总数。

可知：$E[c_xy]=1/m$，$C_{x}=\sum_{y \in T-\{x\}} c_{x y}$

可证：
$$
\begin{aligned}
E\left[C_{x}\right] &=E\left[\sum_{y \in T-\{x\}} c_{x y}\right] \\
&=\sum_{y \in T-\{x\}} E\left[c_{x y}\right] \\
&=\sum_{y \in T-\{x\}} 1 / m \\
&=\frac{n-1}{m} . 
\end{aligned}
$$

## 4. Constructing a set of universal hash functions 

Let `m` be prime.Decompose key `k` into `r + 1` digits, each with value in the set `{0, 1, …, m–1}`. That is, let $k = 〈 k_0, k_1, …, k_r 〉$, where $0 ≤ ki < m$.将k进行“m进制表示”。



**Randomized strategy**

Pick $a = 〈 a_0, a_1, …, a_r 〉$ where each $a_i$ is chosen **randomly** from {0, 1, …, m–1}.

Define $h_{a}(k)=\sum_{i=0}^{r} a_{i} k_{i} \bmod m$ 对k和a做点积再对m取余。

How big is $H=\{h_a\}$, $|H|=m^{r+1}$



**Theorem.** The set $H = {h_a}$ is universal.

**Proof.** Suppose that $x = 〈x_0, x_1, …, x_r 〉$ and$ y = 〈y_0, y_1, …, y_r 〉$ be distinct keys. Thus, they differ in at least one digit position, wlog position 0.（假设为0位置）For how many $h_a ∈ H$ do x and y collide. We must have$h_a(x)=h_a(y)$. which implies that:$\sum_{i=0}^{r} a_{i} x_{i} \equiv \sum_{i=0}^{r} a_{i} y_{i} \quad(\bmod m)$,
$$
\sum_{i=0}^{r} a_{i}\left(x_{i}-y_{i}\right) \equiv 0 \quad(\bmod m)
$$

$$
a_{0}\left(x_{0}-y_{0}\right)+\sum_{i=1}^{r} a_{i}\left(x_{i}-y_{i}\right) \equiv 0 \quad(\bmod m)
$$

$$
a_{0}\left(x_{0}-y_{0}\right) \equiv-\sum_{i=1}^{r} a_{i}\left(x_{i}-y_{i}\right) \quad(\bmod m)
$$

因为假设了$x_0\neq y_0$，所以存在$(x_0-y_0)^{-1}$，所以：
$$
a_{0} \equiv\left(-\sum_{i=1}^{r} a_{i}\left(x_{i}-y_{i}\right)\right) \cdot\left(x_{0}-y_{0}\right)^{-1} \quad(\bmod m)
$$
可以看出$a_0$是由其他$a_i$决定的，其他$a_i$确定使得collide的$a_0$就确定了。

如果发生碰撞，the number of h为$m^r*1=|H|/m$.证明为全域哈希。







**Fact from number theory**

**Theorem.**  Let m be prime. For any $z ∈ Z_m$ such that $z ≠ 0$, there exists a unique $z^{–1} ∈ Z_m$ such that:$z \cdot z^{-1} \equiv 1 \quad(\bmod m)$

<img src="https://i.bmp.ovh/imgs/2021/03/c0d884026a0bece0.png" style="zoom:67%;" />

如果不是质数就不成立。



## 5. Perfect hashing

Given a set of n keys, construct a static hash table of size $m = O(n)$ such that `SEARCH` takes $\Theta(1)$ time in the worst case.固定keys静态表$O(1)$时间查找。



**IDEA:** Two level scheme with universal hashing at both levels.No collisions at level 2.

<img src="https://i.bmp.ovh/imgs/2021/03/5a9f5a1ed1076a16.png" style="zoom:67%;" />

 如果有$n_i$个项被同时哈希到一级表的槽i，那么我们将有$m_i=n_i^2$个槽在二级表。



**Theorem.** Let H be a class of universal hash functions for a table of size $m = n^2$. Then, if we use a random $h ∈ H$ to hash n keys into the table, the expected number of collisions is at most 1/2. 如果使用全域哈希$m = n^2$，如果随机采样$h ∈ H$ 期望碰撞数为1/2.

**Proof** 

<img src="https://i.bmp.ovh/imgs/2021/03/205afe16921034e7.png" style="zoom:67%;" />

**马尔可夫不等式（Markov’s inequality）**

 for any nonnegative random variable X, we have $Pr\{X>=t\}<=E[X]/t$

<img src="https://i.bmp.ovh/imgs/2021/03/6905c87427f2ea37.png" style="zoom:50%;" />



**Corollary**. The probability of no collisions is at least 1/2. 

应用马尔可夫不等式，设置t=1， the probability of 1 or more collisions is at most 1/2。

Thus, just by testing random hash functions in H, we’ll quickly find one that works. 

目标是创建静态表，所以这样证明很容易找到合适的哈希函数。



**Analysis of storage**

For the level-1 hash table T, choose m = n, and let ni be random variable for the number of keys that hash to slot i in T.By using $n_i^2$ slots for the level-2 hash table Si, the expected total storage required for the two-level scheme is therefore 
$$
E\left[\sum_{i=0}^{m-1} \Theta\left(n_{i}^{2}\right)\right]=\Theta(n)
$$
since the analysis is identical to the analysis from recitation of the expected running time of **bucket sort**.