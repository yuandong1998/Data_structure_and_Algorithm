# Lec15 动态规划，最长公共子序列



## 1.Longest common  subsequence

**最长公共子序列**：给两个序列`x[1..m]`和`y[1..n]`，找到两者之间最长的公共子序列。

x: ABCBDAB；y:BDCABA。可以看出BCBA|BDAB|BCAB=LCS(x,y)。



**Brute-force LCS algorithm**

检查x中所有的子序列在y中是否存在。一个子序列检查需要$O(n)$的时间，x中有$2^m$的子序列，最坏运行时间为：$O(n2^m)$.



**Towards a better algorithm**

考虑x,y的前缀。定义$C[i,j]=|LCS(x[1..i]),y[1..j]|$。然后$c[m,n]=|LCS(x,y)|$。

转换公式：$c[i, j]=\left\{\begin{array}{ll}
c[i-1, j-1]+1 & \text { if } x[i]=y[j], \\
\max \{c[i-1, j], c[i, j-1]\} & \text { otherwise. }
\end{array}\right.$

证明：略。



## 2. Optimal substructure

最优子结构：问题（实例）的最佳解决方案包含子问题的最佳解决方案。

例子：如果$z=LCS(x,y)$，那么任何z的前缀是一个x前缀与y前罪的LCS。



**Recursive algorithm for LCS**

```
LCS(x,y,i,j)
	if x[i]=y[j] then
		c[i,j]=LCSV(x,y,i-1,j-1)+1
	else
		c[i,j]=max{LCS(x,y,i-1,j),LCS(x,y,i,j-1)}
```



## 3. Overlapping subproblems

重叠子问题：递归解决方案包含多次重复的“少量”独特子问题。两个长度为m和n的字符串的不同LCS子问题的数量仅为$mn$

Memoization : 计算完一个子问题的解决方案后，将其存储在表中。后续调用检查表以避免重做工作。

```
LCS(x,y,i,j)
	if c[i,j]=NIL
	if x[i]=y[j] then
		c[i,j]=LCSV(x,y,i-1,j-1)+1
	else
		c[i,j]=max{LCS(x,y,i-1,j),LCS(x,y,i,j-1)}
```



IDEA：自下而上计算表格。

<img src="https://i.bmp.ovh/imgs/2021/03/ad176424e959bae4.png" style="zoom:67%;" />

* Time=$\Theta(mn)$
* Space=$\Theta(mn)$

可以优化到$O(min\{m,n\})$