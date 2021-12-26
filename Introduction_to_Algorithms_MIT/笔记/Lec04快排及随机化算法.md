# Lec04快速排序



## 1. Quicksort

* Proposed by C.A.R. Hoare in 1962.

* Divide-and-conquer algorithm.

* Sorts “in place” (like insertion sort, but not like merge sort).

* Very practical (with tuning).



## 2. Divide and conquer

快排n个元素的数组

1. Divide：选取pivot x，将数组中小于等于x的放在x的左边，大于等于的放在x的右边。

2. Conquer：递归的排两个子数组。

3. Combine：花销小。

   

## 3. Partitioning

```
PARTITION(A,p,q)
	x=A[p]
	i=p
	for j in [p+1,q]
		do if A[j]<=x
			then i=i+1
				exchange(A[i],A[j])
	exchange(A[p],A[i])
	return i
```



Pseudocode for quicksort

```
QUICKSORT(A,p,r)
	if p<r
		then q=PARTITION(A,p,r)
		QUICKSORT(A,p,q-1)
		QUICKSORT(A,q+1,r)
```



## 4. Worst-case analysis

worse-case 已经排序或者逆序的情况下。划分的其中一边为0。

$T(n)=T(0)+T(n-1)+\Theta(n)=T(n-1)+\Theta(n)=\Theta(n^2)$



## 5. Best-case analysis

如果幸运的话，平均划分(evenly)。

$T(n)=2T(n/2)+\Theta(n)=\Theta(n\lg n)$



如果9 1划分：

$T(n)=T(\frac{1}{10}n)+T(\frac{9}{10}n)+\Theta(n)$



## 6. More intuition

如果在lucky和unlucky交替进行。

$L(n)=2U(n/2)+\Theta(n)$

$U(n)=L(n-1)+\Theta(n)$ 

$L(n)=2(L(n/2-1)+\Theta(n/2))+\Theta(n)=\Theta(n\lg n)$ （2式子替换到1式替换）



## 7. Randomized quicksort

1. Partition around a random element.
2. Running time is independent of the input order.
3. No specific input elicits the worst-case behavior.
4. The worst case is determined only by the output of a random-number generator.

$$
\begin{aligned}
E[T(n)] &=E\left[\sum_{k=0}^{n-1} X_{k}(T(k)+T(n-k-1)+\Theta(n))\right] \\
&=\sum_{k=0}^{n-1} E\left[X_{k}(T(k)+T(n-k-1)+\Theta(n))\right] \\
&=\sum_{k=0}^{n-1} E\left[X_{k}\right] \cdot E[T(k)+T(n-k-1)+\Theta(n)] 独立的可以分开\\
&=\frac{1}{n} \sum_{k=0}^{n-1} E[T(k)]+\frac{1}{n} \sum_{k=0}^{n-1} E[T(n-k-1)]+\frac{1}{n} \sum_{k=0}^{n-1} \Theta(n) \\ 
&=\frac{2}{n} \sum_{k=1}^{n-1} E[T(k)]+\Theta(n) \quad \begin{array}{l}
\end{array}
\end{aligned}
$$

**Prove:** $E[T(n)]<=an\lg n$ for constant a>0

**Use fact** $\sum_{k=2}^{n-1} k \lg k \leq \frac{1}{2} n^{2} \lg n-\frac{1}{8} n^{2}$

**Substitution method**
$$
\begin{aligned}
E[T(n)] & \leq \frac{2}{n} \sum_{k=2}^{n-1} a k \lg k+\Theta(n) \\
&=\frac{2 a}{n}\left(\frac{1}{2} n^{2} \lg n-\frac{1}{8} n^{2}\right)+\Theta(n) \\
&=a n \lg n-\left(\frac{a n}{4}-\Theta(n)\right) \\
& \leq a n \lg n
\end{aligned}
$$
如果a选择足够大，$an/4$大过$\Theta(n)$



## 8. Quicksort in practice

通常比合并排序快两倍

快排通过代码微调可以提升

Quicksort behaves well even with caching and virtual memory.