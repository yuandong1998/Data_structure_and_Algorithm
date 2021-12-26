# Lec10 平衡搜索树



## 1. Balanced search trees

**Balanced search tree:** A search-tree data structure for which a height of $O(\lg n)$ is guaranteed when implementing a dynamic set of `n` items.

Examples:

* AVL trees

* 2-3 trees 
* 2-3-4 trees
* B-trees 
* Red-black trees 



## 2. Red-black trees 

This data structure requires an extra one bit `color` field in each node. 

**Red-black properties:** 

* Every node is either red or black.
* The root and leaves (NIL’s) are black. 
*  If a node is red, then its parent is black.
* All simple paths from any node x to a descendant leaf have the same number of black nodes = black-height(x ).



## 3. Height of a red-black tree

**Theorem.** A red-black tree with n keys has height $h\leq 2\lg(n+1)$.

**Proof：**（书上采用的是induction的方法证明）

INTUITION :

1. Merge red nodes into their black parents. 
2. This process produces a tree in which each node has 2, 3, or 4 children.
3. The 2-3-4 tree has uniform depth h′ of leaves.
4. We have h′ ≥ h/2, since at most half the leaves on any path are red.
5. The number of leaves in each tree is

$$
\begin{aligned}
n+1 & \geq2^{h'}\\
\lg (n+1) &\geq h'\geq h/2\\
h&\leq 2\lg(n+1)
\end{aligned}
$$



**Query operations**

The queries SEARCH, MIN, MAX, SUCCESSOR, and PREDECESSOR all run in $O(\lg n)$ time on a red-black tree with n nodes.



**Modifying operations**

The operations INSERT and DELETE cause modifications to the red-black tree: 

- the operation itself, 
- color changes, 
- restructuring the links of the tree via “rotations”. 



## 4. Rotations 

<img src="https://i.bmp.ovh/imgs/2021/03/c1d1c45335eecca3.png" style="zoom:50%;" />



##  5. Insertion 

**IDEA:** Insert x in tree. Color x red. Only red-black property `3` might be violated. Move the violation up the tree by recoloring until it can be fixed with rotations and recoloring.

 

**Pseudocode:**

<img src="https://i.bmp.ovh/imgs/2021/03/cd34bdf8902df62b.png" style="zoom:67%;" />

**三种情况**

<img src="https://i.bmp.ovh/imgs/2021/03/44a459bb34ba3254.png" style="zoom:50%;" />

<img src="https://i.bmp.ovh/imgs/2021/03/23b5148046e6a6c4.png" style="zoom:50%;" />

<img src="https://i.bmp.ovh/imgs/2021/03/38afb328867bccb9.png" style="zoom:50%;" />

**Analysis**

* Case 1只对节点重新着色
* 如果Case 2,3出现进行1或2次旋转，然后结束



Running time：$O(\lg n)$ with $O(1)$ rotations.

RB-DELETE：和插入具有渐进相同的运行时间和旋转次数。

