# Lec06 顺序统计、中值

## 1. Order statistics

选出`n`个元素中第`i`小的数，`i=1:minimum`，`i = n: maximum`，`i = ⎣(n+1)/2⎦ or ⎡(n+1)/2⎤: median`

很容易想到的一个方法是先排序在索引第`i`个元素。复杂度：$\Theta(n\lg n)$



## 2. Randomized divide-and conquer algorithm

**伪代码**

```
RAND-SELECT(A,p,q,i) //ith smallest of A[p...q]
	if p=q then return A[p]
	r=RAND-PARTITION(A,p,q)
	k=r-p+1 //k=rank(A[r])
	if i=k then return A[r]
	if i<k
		then return RAND-SELECT(A,p,r-1,i)
		else return RAND-SELECT(A,r+1,q,i-k)
```



**Analysis of expected time**

划分指示器
$$
X_{k}=\left\{\begin{array}{ll}
1 & \text { if PARTITION generates a } k: n-k-1 \text { split, } \\
0 & \text { otherwise. }
\end{array}\right.
$$

$$
\begin{aligned}
T(n)=&\left\{\begin{array}{cl}
T(\max \{0, n-1\})+\Theta(n) & \text { if } 0: n-1 \text { split, } \\
T(\max \{1, n-2\})+\Theta(n) & \text { if } 1: n-2 \text { split, } \\
\vdots \\
T(\max \{n-1,0\})+\Theta(n) & \text { if } n-1: 0 \text { split }
\end{array}\right.\\
&=\sum_{k=0}^{n-1} X_{k}(T(\max \{k, n-k-1\})+\Theta(n))
\end{aligned}
$$

<img src="https://i.bmp.ovh/imgs/2021/02/bf9407c00e877ed9.png" style="zoom:67%;" />

再用替换法证明，$E[T(n)]\leq cn$for constant c>0。
$$
\begin{aligned}
E[T(n)] & \leq \frac{2}{n} \sum_{k=\lfloor n / 2\rfloor}^{n-1} c k+\Theta(n) \\
& \leq \frac{2 c\left(\frac{3}{8} n^{2}\right)+\Theta(n)}{n} \\
&=c n-\left(\frac{c n}{4}-\Theta(n)\right) \\
& \leq c n
\end{aligned}
$$
if c is chosen large enough so that cn/4 dominates the Θ(n)



**Summary of randomized order-statistic selection**

* 线性期望时间
* worst case：$\Theta(n^2)$



## 3. Worst-case linear-time order statistics

[Blum, Floyd, Pratt, Rivest,  Tarjan] 

IDEA: Generate a good pivot recursively.

```
SELECT(i, n)
1. Divide the n elements into groups of 5. Find the median of each 5-element group by rote.
2. Recursively SELECT the median x of the ⎣n/5⎦ group medians to be the pivot.
3. Partition around the pivot x. Let k = rank(x).
4. if i = k then return x
	elseif i < k
		then recursively SELECT the ith smallest element in the lower part
	else recursively SELECT the (i–k)th smallest element in the upper part
	
3 4步和RAND-SELECT一样
```



**Analysis**

<img src="https://i.bmp.ovh/imgs/2021/02/543683de9884cb03.png" style="zoom:67%;" />

 

<img src="https://i.bmp.ovh/imgs/2021/02/85706540dcd02af4.png" style="zoom:67%;" />



* 实际上，此算法运行缓慢，因为n前面的常数很大
* 随机算法更加实用。

练习：为什么不分成3组？