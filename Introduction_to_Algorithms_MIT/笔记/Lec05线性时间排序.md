# Lec05线性时间排序

## 1.Sorting Lower Bounds

insertion sort, merge sort, quicksort, heapsort 都只能对两个元素进行比较来确定顺序。

**prove** ：比较排序算法的最小时间的是$O(n\lg n)$

通过Decision-tree来证明，Decision-tree入下所示。节点`1:2`表示数组中A[1]和A[2]进行比较，向左表示A[1]<=A[2]，向右表示A[1]>=A[2]。所有排序的比较过程都可以用树中的一条路径表示。

<img src="https://i.bmp.ovh/imgs/2021/02/d15b4f2287ee343c.png" style="zoom:50%;" />



**Theorem:** Any decision tree that can sort n elements must have height Ω(n lg n).

**proof：** 树中的叶子树$>=n!$因为有$n!$个可能的排列组合数。$n!\leq 2^g,h\geq\Omega(n\lg n)$
$$
\begin{aligned}
h & \geq \lg (n !)  \\
& \geq \lg \left((n / e)^{n}\right) (Stirling’s formula)\\
&=n \lg n-n \lg e \\
&=\Omega(n \lg n)
\end{aligned}
$$


Heapsort and merge sort are asymptotically optimal comparison sorting algorithms.



## 2. Sorting in linear time

### 2.1 Counting sort

对数组中的树进行了假设。

**Input:** $A[1,...,n],A[i]\in \{1,2,...,k\}$

**Output:**$B[1,...,n]$

**Auxiliary storage:** $C[1..k]$





```
for i ← 1 to k
	do C[i] ← 0
for j ← 1 to n
	do C[A[ j]] ← C[A[ j]] + 1 ⊳ C[i] = |{key = i}|
for i ← 2 to k
	do C[i] ← C[i] + C[i–1] ⊳ C[i] = |{key ≤ i}|
for j ← n downto 1
	do B[C[A[j]]] ← A[j]
		C[A[j]] ← C[A[j]] – 1
```

**时间复杂度：** $\Theta(n+k)$

**Stable sorting：**it preserves the input order among equal elements.



## 2.2 Radix sort基数排序

digit-by-digit sort，sort on least-significant digit first with auxiliary stable sort.



**Correctness of radix sort**

假设低`t-1`位都已经排序，对第`t`位排序，在`t`位不同的数按照顺序排序，相同的数的顺序和输入一样就可以保证正确的排序。



**Analysis of radix sort**

排序n个单词，每个单词有b个bits，以$2^r$为一位有$b/r$位。Counting sort的复杂度$\Theta(n+k)$，所以时间复杂度为$T(n,b)=\Theta(\frac{b}{r}(n+2^r))$，选择合适的r来最小化$T(n,b)$，通过求导的方法，$r=\lg n$从而$T(n,b)=\Theta(bn/\lg n)$，对于数组大小在$[0,n^d-1]$之间，$b=d\lg n$ ，radix sort的复杂度为$\Theta(dn)$。





