# Lec12跳跃表

## 1. Skip Lists

跳跃表：随机化动态搜索结构，简单容易实现。$O(\lg n)$的期望运行时间， 并且有很大的概率$1-\frac{1}{e^\alpha}$。

其他高效的动态搜索结构，比如树堆、红黑树、B-trees。



**sorted linked list**

search:$\Theta(n)$ time，如何提速呢？



**Two linked list**

IDEA：新加一个list来作为“快速通道”。



<img src="https://i.bmp.ovh/imgs/2021/03/5c89bcbbdc1a8ea5.png" style="zoom:50%;" />

search(x)

1. 从list L1向右搜索，直到搜索过头
2. 向下到list L2
3. 向右搜索，直到搜索到元素



**Analysis**

粗略估计：$|L1|+\frac{|L2|}{|L1|}$. $|L2|=n$

最小化： $|L1|=\sqrt n$

 

2 sort lists: $2 \sqrt n$

3 sort lists: $3n^{1/3}$

k sorted lists: $kn^{1/k}$

$\lg n$ sorted lists:$\lg n*n^{1/\lg n}=2\lg n$



$\lg n$ sorted lists 像一个二分树。

**Ideal skip list** is this $\lg n$ linked list structure.

上一次与下一层的比为1:2，负无穷存在所有表中的最左边。

```
INSERT(x)
最底层插入的有所有元素。以1/2的概率决定下一层是否插入。

DELETE(x)
删除所有表中的x
```

<img src="https://i.bmp.ovh/imgs/2021/03/614985fbff593b99.png" style="zoom:50%;" />

不仅平均为$O(\lg n)$，并且高概率为$O(\lg n)$



## 2. With-high-probability theorem

**THEOREM:** 有很高的概率，每次搜索的时间消耗是$O(\lg n)$



**Boole’s inequality**

<img src="https://i.bmp.ovh/imgs/2021/03/0aa140691c4a2ad3.png" style="zoom:50%;" />



如果$k=n^{O(1)}$，每一个$E_i$都具有高概率，那么$E_1 \cap E_2,...,\cap E_k$.

<img src="https://i.bmp.ovh/imgs/2021/03/c19ba3e532edd693.png" style="zoom:67%;" />

