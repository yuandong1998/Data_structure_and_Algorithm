# Lec11 扩充的数据结构、动态有序统计和区间树

Augmenting Data Structures(扩充的数据结构)



## 1. Dynamic order statistics

**实现功能**

`OS-SELECT(i, S)`: returns the `ith` smallest element in the dynamic set S

`OS-RANK(x, S)`: returns the rank of x ∈ S in the sorted order of S’s elements.



**IDEA**: 对set S采用红黑树，但是在节点里保存子树的大小。`size[x] = size[left[x]] + size[right[x]] + 1`.



实现的一个技巧：对NIL采用sentinel(dummy record)，`size[NIL]=0`.

```
OS-SELECT(x,i) //ith smallest element in the subtree rooted at x 

k=size[left[x]]+1 //k=rank(x)
if i=k then return x
if i<k
	then return OS-SELECT(left[x],i)
	else return OS-SELECT(right[x],i-k)
```

运行时间为$O(h)=O(\lg n)$.



为什么保存树的大小而不是直接是值得rank，因为Insert和DELETE，当修改红黑树时，很难维护它们。插入或删除时更新子树大小。

插入时修改树的大小值，然后需要重新平衡。

* Recolorings: 对树的大小没有影响

* Rotations: $O(1)$的时间修复树

  <img src="https://i.bmp.ovh/imgs/2021/03/3dff42f57651aaf9.png" style="zoom:50%;" />

  

## 2. Methodology

1. 选择基础数据结构（红黑树）。
2. 确定要存储在数据结构中的其他信息（子树大小）
3. 确认可以保留此信息以进行修改操作（RBINSERT，RB-DELETE-不要忘记轮换）。
4. 开发使用该信息的新动态集操作（OS-SELECT和OS-RANK）。

这些步骤是指导性的，而不是严格的规则。



## 3. Interval trees

目标：维护动态间隔集，例如时间间隔

Query：对于给定的查询间隔`i`，在集合中找到一个与`i`重叠的间隔。



**Following the methodology**

1. 选择基础数据结构：红黑树key设为低端点。

2. 确定要存储在数据结构中的其他信息。在每个节点x中存储以`x`为根的子树中的最大值`m[x]`以及与该键对应的间隔`int[x]`。

   <img src="https://i.bmp.ovh/imgs/2021/03/d8e5f8156ad9ba3a.png" style="zoom:50%;" />

   

3. 验证可以保留此信息以用于修改操作。

   1. Insert：沿着树插下来。

   2. Rotations：修复需要$O(1)$时间。

      <img src="https://i.bmp.ovh/imgs/2021/03/c0f5d6775e8f7f43.png" style="zoom:50%;" />

4. 开发使用该信息的新动态集操作。

   <img src="https://i.bmp.ovh/imgs/2021/03/b0ee510dd13b5e0f.png" style="zoom:50%;" />



**Analysis**

查询一次需要$O(\lg n)$，查询所有：搜索，列出，删除，重复。需要$O(k\lg n)$，最好的算法为$O(k+\lg n)$.



**Correctness**

<img src="https://i.bmp.ovh/imgs/2021/03/c8ab820678489f8c.png" style="zoom:50%;" />

