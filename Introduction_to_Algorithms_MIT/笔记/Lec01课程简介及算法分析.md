# Lec01 课程简介及算法分析

对应书上的章节：Chapters 1-2

## 1.介绍

### 1.1 先修课程

离散数学、概率论、编程课程

### 1.2 算法分析

计算机程序性能和资源使用的理论研究（尤其关注性能）。

### 1.3 比性能更重要的因素

比如有正确性、简洁性、可维护性、编程成本、稳定性、功能性、模块化、安全性、可扩展性、用户友好度等。

### 1.4 算法的重要性

- 算法将不可行变为可行。
- 算法是一种描述程序行为的语言。



## 2. 排序问题

### 2.1 Insertion sort

**伪代码（pseudocode）**

```
for j ← 2 to n
    do key ← A[j]
    i ← j-1
    while i > 0 and A[i] >key
        do A[i+1] ← A[i]
        i ← i-1
    A[i+1] ← key
```

**运行时间（Running time）**

* 取决于数据，有序的数据速度更快。
* 取决于数据规模大小。
* 更关注运行时间的上限，更有保证。

**分析方法（Kinds of analyses）**

* 最坏情况：取决于计算机性能，通常描述不使用绝对速度，关注相对速度。
* 平均情况：需要假设数据分布
* 最好情况：有迷惑性
* 渐近分析（Asymptotic Analysis）
  * $\Theta(g(n))={f(n):存在正的常数c_1,c_2已经n_0使得对于所有的n>=n_0都有0\leq c_1g(n)\leq f(n)\leq c_2g(n)}$，也就是去掉函数的低阶项和最高阶项系数。
  * 关注随模型增长的增长情况



### 2.2 Merge Sort

**伪代码**

```
MERGE-SORT A[1...n]
1.if n=1,done
2.recursively sort A[1..[n/2]] and A[[n/2]+1,...,n]
3.merge 2 sorted lists
```

**算法分析**

$T(n)=2(T/2)+\Theta(n)$

$T(n)=2(T/2)+c n$

**递归树 Recursion tree**

<img src="https://ftp.bmp.ovh/imgs/2021/03/20e766da834288c8.png" style="zoom:67%;" />