# Lec03 分治法

[TOC]

## 1. 分治法

1. Divide：将问题划分为多个子问题
2. Conquer：通过递归解决子问题
3. Combine：将子问题的解合并为大问题的解



## 2. Merge sort

```
algorithm：
1. Divide：划分为2个数组
2. Conquer：递归的排序两个数组
3. Combine：将两个有序数组合并，需要线性时间
```

$T(n)=2T(n/2)+\Theta(n)$ 根据主方法，$T(n)=\Theta(n\lg n)$



## 3. Binary search

```
algorithm:
1. Divide：找到中间元素
2. Conquer：递归查找其中一个子数组
3. Combine：合并
```

$T(n)=T(n/2)+\Theta(1)$ 根据主方法，$T(n)=\Theta(\lg n)$



## 4. Powering a number

algorithm:

<img src="https://i.bmp.ovh/imgs/2021/01/bdd497742fae9942.png" style="zoom:50%;" />

$T(n)=T(n/2)+\Theta(1)$ 根据主方法，$T(n)=\Theta(\lg n)$



## 5. Fibonacci numbers

**朴素的递归算法（Naive recursive algorithm）** $T(n)=\Omega(\phi^n),\phi=(1+\sqrt 5)/2$ golden ratio。

**自底向上（Bottom-up）：**从下往上计算。$T(n)=\Theta(n)$

**朴素的递归平方（Naive recursive squaring）：** 通过公式计算，$F_n=\phi^n/\sqrt 5$最近的整数。但是这个方法不安全，浮点运算容易产生舍入误差。

 **递归平方（Recursive squaring）：** 通过如下的公式计算，通过乘法通过二分法优化 $T(n)=\Theta(\lg n)$，可以通过归纳法证明。
$$
\left[\begin{array}{cc}
F_{n+1} & F_{n} \\
F_{n} & F_{n-1}
\end{array}\right]=\left[\begin{array}{cc}
1 & 1 \\
1 & 0
\end{array}\right]^{n}
$$


## 6. Matrix multiplication

**标准算法（Standard algorithm）**

```
for i in [1,n]:
	do for j in [1,n]:
		do cij=0
			for k in [1,n]:
				do cij=cij+aik*akj
```

$T(n)=\Theta(n^3)$



**分治法（Divide-and-conquer algorithm）**

将nxn的矩阵分为4个$(n/2)*(n/2)$的子矩阵，如下图所示：

<img src="https://i.bmp.ovh/imgs/2021/01/58564478786e721a.png" style="zoom: 50%;" />

$T(n)=8T(n/2)+\Theta(n^2)$，主方法得$T(n)=\Theta(n^3)$，没有改进。



**Strassen’s algorithm：**将上面提到的方法乘法次数从8降到7。
$$
\begin{array}{ll}
P_{1}=a \cdot(f-h) & r=P_{5}+P_{4}-P_{2}+P_{6} \\
P_{2}=(a+b) \cdot h & s=P_{1}+P_{2} \\
P_{3}=(c+d) \cdot e & t=P_{3}+P_{4} \\
P_{4}=d \cdot(g-e) & u=P_{5}+P_{1}-P_{3}-P_{7} \\
P_{5}=(a+d) \cdot(e+h) \\
P_{6}=(b-d) \cdot(g+h) \\
P_{7}=(a-c) \cdot(e+f)
\end{array}
$$
进行7次乘法，18次加法\减法。$T(n)=8T(n/2)+\Theta(n^2)$，由主方法计算得$T(n)=\Theta(n^{lg 7})$。



## 7. VLSI tree layout

problem：使用最小的面积将具有n个叶子的完整二叉树嵌入网格中。

以下介绍两种方法：

方法一：

<img src="https://i.bmp.ovh/imgs/2021/01/985a319949fe5f07.png" style="zoom:50%;" />



方法二：

<img src="https://ftp.bmp.ovh/imgs/2021/03/25b53265a95180f2.png" style="zoom:50%;" />