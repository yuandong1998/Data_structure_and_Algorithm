# Lec02 渐进符号、递归及解法

对应书的章节：Chapters 3-4, excluding section 4.6

## 1. 渐进符号（Asymptotic Notation）

### 1.1 $O$-notation （upper bounds）

$f(n)=O(g(n))$ 如果存在常量$c>0,n_0>0$对所有的$n\geq n_0$都有$0\leq f(n)\leq cg(n)$。

比如 $2n^2=O(n^3)$，这个符号可以用$\leq$理解，表示$g(n)$是$f(n)$的上界。



### 1.2 $\Omega$-notation（lower bounds）

$f(n)=\Omega(g(n))$ 如果存在常量$c>0,n_0>0$对所有的$n\geq n_0$都有$0\leq cg(n) \leq f(n) $。

比如 $\sqrt n=\Omega(\lg n)$，这个符号可以用$\geq$理解，表示下界。



### 1.3 $\Theta$-notation（tight bounds）

$\Theta(g(n))=O(g(n))\cap \Omega(g(n))$

比如$\frac{1}{2}n^2-2n=\Omega(n^2)$，可以用$=$理解。



### 1.4 $o$-notation

$f(n)=o(g(n))$ 如果存在常量$c>0,n_0>0$对所有的$n\geq n_0$都有$0\leq f(n)< cg(n)$。

比如$2n^2=o(n^3)$，可以用<理解。



### 1.5 $\omega$-notation

$f(n)=\omega(g(n))$ 如果存在常量$c>0,n_0>0$对所有的$n\geq n_0$都有$0\leq cg(n) < f(n) $。

比如$\sqrt n=\omega(\lg n)$，可以用>理解。



## 2. 递归（Recurrences）

### 2.1 代换法（Substitution method）

```
1. Guess 猜测结果。
2. verify 归纳验证。
3. solve 求系数。
```

例子：$T(n)=4T(n/2)+n;T(1)=\Theta(1)$

（一）假设$T(n)=O(n^3)$

1. 假设$T(n)=O(n^3)$ 则$T(k)\leq ck^3$ for $k<n$ 

2. $T(n)=4T(n/2)+n\leq4c(n/2)^3+n=cn^3-((cn^3)/2-n)$ 构造成 desired-residual，就是假设的减去剩下的。
3. 要使得假设成立，则$cn^3/2-n\geq0$，所以$c\geq2，n\geq1$不等式成立。
4. 我们还必须处理初始条件，$T(1)=\Theta(1)\leq c*1^3$，当c取足够大的数时不等式成立。（This bound is not tight!）

（二）假设$T(n)=O(n^2)$

1. 假设$T(n)=O(n^2)$ 则$T(k)\leq ck^2$ for $k<n$
2. $T(n)=4T(n/2)+n\leq4c(n/2)^2+n=c*n^2-(-n)$
3. 要使假设成立需要$-n>0$，不能成立

（三）加强归纳假设

1. 假设$T(n)=O(n^2)$ 则$T(k)\leq c_1k^2-c_2k$ for $k<n$
2. $T(n)=4T(n/2)+n\leq c_1n^2-c_2n$
3. 要使假设成立，$c_2\geq 1$
4. 验证初始条件$T(1)=\Theta(1)\leq c_1*1^2-c_2*1$，$c_1$足够大不等式成立。

求$T(n)$的下界用类似的方法。

### 2.2 递归树方法（Recursion-tree method）

这个方法不够严谨，比较好的解题过程应该是用递归树法求出结果后再用代换法验证。

<img src="https://ftp.bmp.ovh/imgs/2021/01/33bc3bf17a284dc8.png" style="zoom: 50%;" />



### 2.3 主方法（The master method）

主方法解决形如$T(n)=aT(n/b)+f(n)$的式子，并且$a\geq1,b\geq1$，$f(n)$是趋近为正的。

1. **case1：**$f(n)=O(n^{\log_ba-\epsilon}),\epsilon>0$，$f(n)$ 比$n^{\log_ba}$的增长慢$n^\epsilon$多项式级，**Solution：** $T(n)=\Theta(n^{log_ba})$
2. **case2：** $f(n)=\Theta(n^{\log_ba}\lg^kn),k\geq 0$ $f(n)$和$n^{log_ba}$有一样的增长速度，**Solution:**$T(n)=\Theta(n^{\log_ba}\lg^{k+1}n)$
3. **case3：** $f(n)=\Omega(n^{\log_ba+\epsilon}),\epsilon>0$，并且存在$c<1,af(n/b)\leq cf(n)$ $f(n)$ 比$n^{\log_ba}$的增长快$n^\epsilon$多项式级，**solution：** $T(n)=\Theta(f(n))$



**用递归树来理解主方法**

**case1:**

<img src="https://ftp.bmp.ovh/imgs/2021/01/d96bb64eef94c195.png" style="zoom:50%;" />



**case2：**

<img src="https://ftp.bmp.ovh/imgs/2021/01/48ae662c70a10496.png" style="zoom:50%;" />



**case3：**

<img src="https://ftp.bmp.ovh/imgs/2021/01/d9e63987e5069e08.png" style="zoom:50%;" />





## Appendix: geometric series

$$
\begin{array}{c}
1+x+x^{2}+\cdots+x^{n}=\frac{1-x^{n+1}}{1-x} \text { for } x \neq 1 \\
1+x+x^{2}+\cdots=\frac{1}{1-x} \quad \text { for }|x|<1
\end{array}
$$



