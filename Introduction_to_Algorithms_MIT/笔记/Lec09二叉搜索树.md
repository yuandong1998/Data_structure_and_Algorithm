# Lec09 二叉搜索树

本节介绍Randomly built binary search trees.



## 1. Binary-search-tree sort

二叉搜索树排序过程如下：

<img src="https://i.bmp.ovh/imgs/2021/03/87a24aa456fcd0b8.png" style="zoom:50%;" />



遍历树的时间为$O(n)$，但是构建BST的时间是多少？

BST sort和quick sort很像：BST sort performs the same comparisons as quicksort, but in a different order!



## 2. Expected node depth

Assuming all input permutations are equally likely, we have：（BST sort performs the same comparisons as quicksort）
$$
Average\ node\ depth=\frac{1}{n}E[\sum(\#comparisons\ to\ insert\ node\ i)]=\frac{1}{n}O(n\lg n)=O(\lg n)
$$
但是平均节点深度并不等于树的期望高度。



## 3. Analyzing height

**Jensen’s inequality：** $f(E[X])\leq E[f(x)]$ for any convex function f and random variable X.

**Exponential height：** random variable $Y_n=x^{X_n}$，where $X_n$ is the random varible denoting the height of BST.



**证明：** Prove that $2^{E[X_n]}\leq E[2^{X_n}]=E[Y_n]=O(n^3)$,hence that $E[X_n]=O(\lg n)$



**凸函数(Convex functions)定义**： $f:R->R$ is convex if for all $\alpha,\beta\geq 0$ such that $\alpha+\beta=1$,we have $f(\alpha x+\beta y)\leq \alpha f(x)+\beta f(y)$ for all $x,y\in R$.



**Convexity lemma：** Let $f$ be a convec function,and let $\alpha_1,..,\alpha_n$ be nonnegative real numbers such that$\sum \alpha_k=1$, Then for any real numbers $x_1,...,x_n$,we have$f\left(\sum_{k=1}^{n} \alpha_{k} x_{k}\right) \leq \sum_{k=1}^{n} \alpha_{k} f\left(x_{k}\right)$. 

**proof:** 归纳法证明：
$$
\begin{aligned}
f\left(\sum_{k=1}^{n} \alpha_{k} x_{k}\right) &=f\left(\alpha_{n} x_{n}+\left(1-\alpha_{n}\right) \sum_{k=1}^{n-1} \frac{\alpha_{k}}{1-\alpha_{n}} x_{k}\right) \\
& \leq \alpha_{n} f\left(x_{n}\right)+\left(1-\alpha_{n}\right) f\left(\sum_{k=1}^{n-1} \frac{\alpha_{k}}{1-\alpha_{n}} x_{k}\right) \\
& \leq \alpha_{n} f\left(x_{n}\right)+\left(1-\alpha_{n}\right) \sum_{k=1}^{n-1} \frac{\alpha_{k}}{1-\alpha_{n}} f\left(x_{k}\right)\\
&=\sum_{k=1}^{n} \alpha_{k} f\left(x_{k}\right)\\
\end{aligned}
$$

**Convexity lemma: infinite case**

<img src="https://i.bmp.ovh/imgs/2021/03/9754b4c9b5591036.png" style="zoom:50%;" />

引申到 Jensen’s inequality：

<img src="https://i.bmp.ovh/imgs/2021/03/19c4bf693ea251e6.png" style="zoom:50%;" />

**Analysis of BST height**

Let Xn be the random variable denoting the height of a randomly built binary search tree on n nodes, and let $Y_n = 2^{X_n}$ be its exponential height.

If the root of the tree has rank k, then $X_n=1+max\{X_{k-1},X_{n-k}\}$.Hence, we have$Y_n=2*\{maxY_{k-1},Y_{n-k}\}$.

Define the indicator random variable $Z_{nk}$ as :$Z_{n k}=\left\{\begin{array}{ll}
1 & \text { if the root has rank } k \\
0 & \text { otherwise. }
\end{array}\right.$

Thus, $\operatorname{Pr}\left\{Z_{n k}=1\right\}=\mathrm{E}\left[Z_{n k}\right]=1 / n$, and $Y_{n}=\sum_{k=1}^{n} Z_{n k}\left(2 \cdot \max \left\{Y_{k-1}, Y_{n-k}\right\}\right)$.
$$
\begin{aligned}
E\left[Y_{n}\right] &=E\left[\sum_{k=1}^{n} Z_{n k}\left(2 \cdot \max \left\{Y_{k-1}, Y_{n-k}\right\}\right)\right] \\
&=\sum_{k=1}^{n} E\left[Z_{n k}\left(2 \cdot \max \left\{Y_{k-1}, Y_{n-k}\right\}\right)\right] \\
&=2 \sum_{k=1}^{n} E\left[Z_{n k}\right] \cdot E\left[\max \left\{Y_{k-1}, Y_{n-k}\right\}\right] \\
& \leq \frac{2}{n} \sum_{k=1}^{n} E\left[Y_{k-1}+Y_{n-k}\right] \\
&=\frac{4}{n} \sum_{k=0}^{n-1} E\left[Y_{k}\right] & \begin{array}{c}
\text { Each term appears } \\
\text { twice, and reindex }
\end{array}
\end{aligned}
$$
采用替代法证明$E[Y_n]\leq cn^3$ for some positive constant.
$$
\begin{aligned}
E\left[Y_{n}\right] &=\frac{4}{n} \sum_{k=0}^{n-1} E\left[Y_{k}\right] \\
& \leq \frac{4}{n} \sum_{k=0}^{n-1} c k^{3} \\
& \leq \frac{4 c}{n} \int_{0}^{n} x^{3} d x \\
&=\frac{4 c}{n}\left(\frac{n^{4}}{4}\right)\\
&=\mathrm{cn}^{3}
\end{aligned}
$$
Putting it all together, we have$2^{E\left[X_{n}\right]} \leq E\left[2^{X_{n}}\right]=E[Y_n]\leq cn^3$,since $f(x)=2^x$is convex

可得$E[X_n]\leq 3\lg n+O(1)$.





## 4. Post mortem

<img src="https://i.bmp.ovh/imgs/2021/03/e7fdfbc3719c0181.png" style="zoom:50%;" />

