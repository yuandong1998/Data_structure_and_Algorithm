# Leetcode notebook

记录leetcode上的刷题学习过程，`notebook`目录为各个题目的笔记，`summary`目录是算法的总结。



## TODO LIST

- [ ] 拓扑排序
- [ ] 从给定原材料中找到所有可以做出的菜
- [ ] 一个区间内所有数乘积的缩写
- [ ] 执行所有后缀指令
- [ ] 相同元素的间隔之和
- [ ] 还原原数组
- [ ] 括号问题
- [ ] KMP算法
- [ ] 字典树的总结
- [ ] DFS和BFS



## 需要复习的

- [ ] 字典树



## Algorithm Notes

* [回溯算法(Backtracking)](./summary/Backtracking.md)
* [Rabin-Karp字符串编码](./summary/Rabin-Karp字符串编码.md)
* 二分查找
* 背包算法
* 字符哈希
* 双指针
* 排序算法
* 字典树



## Leetcode Notes Content

★ 简单 ★★ 中等 ★★★ 困难

一、树类型（树的遍历、二叉搜索树、字典树）

* 三种遍历 (迭代与递归，重点是迭代)
  * [二叉树的中序遍历](./notebook/二叉树的中序遍历.md) (栈)
  * [二叉树的前序遍历](./notebook/二叉树的前序遍历.md) （栈）
  * [二叉树的后序遍历](./notebook/二叉树的后序遍历.md) （加入一个变量记录前一个访问的节点）

* [二叉树的层序遍历](./notebook/二叉树的层序遍历.md) （用队列queue和记录当前层的节点个数）
  
* [二叉树的锯齿形层次遍历](./notebook/二叉树的锯齿形层次遍历.md) （采用BFS的方法，并设计一个flag来判断方向，如果从左向右则` temp.push_back(p->val);`，否则`temp.insert(temp.begin(),1,p->val);`）
  
* [二叉搜索树的后序遍历序列](./notebook/二叉搜索树的后序遍历序列.md)  （递归，数组最后的值是根节点，通过根节点可以将数组分为左子树和右子树，通过递归判断子树）

* [不同的二叉搜索树](./notebook/不同的二叉搜索树.md)（动态规划求解；$G(n)=\sum_{i=1}^n G(i-1)*G(n-i)$）

* [不同的二叉搜索树II](./notebook/不同的二叉搜索树II.md) （递归构建；根节点为i，以[1,...,i-1]为构建左子树，以[i+1,...,n]构建右子树，`vector<TreeNode*> helper(int start,int end)`来生成[start,...,end]的所有二叉搜索树）

* [二叉搜索树的第 k 大节点](./notebook/二叉搜索树的第 k 大节点.md)（剑指offer，按照“右-中-左”遍历树，每遍历一个节点k--，进行计数，直到k==0）

* [二叉搜索树与双向链表](./notebook/二叉搜索树与双向链表.md) （二叉搜索树的中序遍历为递增序列，遍历时设置前驱节点`pre`，当前节点`cur`，构建排序列表）

* [二叉树的最近公共祖先](./notebook/二叉树的最近公共祖先.md) （当前节点为空或等于p或q则返回当前节点，递归左右子树，左右子树查到节点都不为空，当前节点为最近公共祖先，左右子树其中一个不为空，则返回非空节点；$(f_{lson}\&\&f_{rson})||((x==p||x==q)\&\&(f_{lson}||f_{rson}))$）

* [树的子结构](./notebook/树的子结构.md) （递归，（B为A从A根节点开始的子结构）||（B为A从A根节点的左子节点开始的子结构）||（B为A从A根节点的右子节点开始的子结构））

* [重建二叉树](./notebook/重建二叉树.md) （前序遍历的第一个节点是根节点，只要找到根节点在中序遍历中的位置，在根节点之前被访问的节点都位于左子树，在根节点之后被访问的节点都位于右子树，由此可知左子树和右子树分别有多少个节点。）

* [二叉树中和为某一值的路径](./notebook/二叉树中和为某一值的路径.md) （ 回溯法，`root->left==NULL && root->right==NULL && root!=NULL && sum-root->val==0`）

* [Populating Next Right Pointers in Each Node](./notebook/Populating_Next_Right_Pointers_in_Each_Node.md) 

* [Sum_of_Distances_in_Tree](./notebook/Sum_of_Distances_in_Tree.md) 

* [实现Trie(前缀树)](./notebook/实现Trie(前缀树).md)  

* [单词频率](./notebook/单词频率.md) （Trie树）

* [★★★ 连接词](./notebook/连接词.md) （首先对`words`根据长度进行从小到大排序，然后从左向右遍历的同时构建字典树并且采用dfs的方法检查是否是连接词。）

  

二、动态规划

* [最小路径和](./notebook/最小路径和.md)

* [股票的最大利润](./notebook/股票的最大利润.md)

* [礼物的最大价值](./notebook/礼物的最大价值.md)（剑指offer）

* [最长不含重复字符的子字符串](./notebook/最长不含重复字符的子字符串.md)（剑指offer）

* [单词拆分](./notebook/单词拆分.md) 2020/8/21

* [单词拆分二](单词拆分二.md) 2020/9/10

* [连续子数组的最大和 ](./notebook/连续子数组的最大和.md) 2020/8/22

* [最长上升子序列](./notebook/最长上升子序列.md) 2020/8/25

* [零钱兑换](零钱兑换.md) 2020/9/10

* [乘积最大子数组](乘积最大子数组.md) 2020/9/11

* [完全平方数](完全平方数.md) 2020/9/11

* [秋叶收藏集](秋叶收藏集.md) 2020/9/12

* [剪绳子](剪绳子.md) 2020/9/13

* [Partition_Equal_Subset_Sum](./notebook/Partition_Equal_Subset_Sum.md) 2020/10/12

* [Palindrome Partitioning IV](./notebook/Palindrome_Partitioning_IV.md) 2021/2/4

* [Coin LCCI](./notebook/Coin.md) 2021/2/8

* [Circus Tower LCCI](./notebook/Circus_Tower.md) 2021/4/12

* [第 k 个数](./notebook/第k个数.md) 2021/4/12

* [恢复空格](./notebook/恢复空格.md) 2021/4/13

* [★★★ 猫和老鼠](./notebook/猫和老鼠.md)

  


三、栈

* [队列的最大值](./notebook/队列的最大值.md)(剑指offer)

* [栈的压入、弹出序列](./notebook/栈的压入、弹出序列md)（剑指offer）2020/8/10

* [★★ 二叉搜索树的后序遍历序列](./notebook/二叉搜索树的后序遍历序列.md)

   



四、链表

* [链表中倒数第k个节点](./notebook/链表中倒数第k个节点.md)（剑指offer）2020/8/10
* [Palindrome Linked List LCCI](./notebook/Palindrome_Linked_list.md) 2020/1/28
* [Intersection of Two Linked Lists LCCI](./notebook/Intersection_of_Two_Linked_Lists.md) 2020/1/28
* [Linked List Cycle LCCI](./notebook/Linked_List_Cycle.md) 2020/1/31
* [LRU缓存结构](./notebook/LRU缓存结构.md) （哈希表+双向链表；哈希表存双向链表的节点）



五、数学

* [表示数值的字符串](./notebook/表示数值的字符串.md)（剑指offer 未完成）



六、广度优先搜索和深度优先搜索

* [被围绕的区域](./notebook/被围绕的区域.md) 2020/8/20
* [Route Between Nodes LCCI](./notebook/Route_Between_Nodes.md) 2021/2/3
* [Paths with Sum LCCI](./notebook/Paths_with_Sum.md) 2021/2/6
* [★★ 01矩阵 ](./notebook/01矩阵.md) （BFS,先将所有的0都加入队列中，然后开始BFS进行搜索）
* [★★★参加会议的最多员工数](./notebook/参加会议的最多员工数.md) （采用两种dfs计算，最后取最大）



七、[回溯算法(Backtracking)](./summary/Backtracking.md)

* [单词搜索**](./notebook/单词搜索.md)
* [子集**](./notebook/子集.md)
* [Eight Queens LCCI]
* [Unique_Paths_3](./notebook/Unique_Paths_3.md)
* [Iterator_for_Combination](./notebook/Iterator_for_Combination.md)
* [Split Array into Fibonacci Sequence](./notebook/Split_Array_into_Fibonacci_Sequence.md)
* [给表达式添加运算符](./notebook/给表达式添加运算符.md) 2021/1/25
* [★★★二叉搜索树序列](./notebook/二叉搜索树序列.md) （采用回溯算法与双向队列`dq`（deque），双向队列维护一个选择列表。每次确定`dq`的size大小再遍历选择。）



八、堆、优先队列（Heap）

* [Top_K_Frequent_Elements ](./notebook/Top_K_Frequent_Elements.md) 
* [数据流中的中位数](./notebook/数据流中的中位数.md) （小根堆存大的一半，大根堆存小的一半）
* [吃苹果的最大数量](./notebook/吃苹果的最大数量.md) （贪心的吃最近腐烂的，用小根堆存苹果的腐烂时间和数量）



九、图

* [Maximal_Network_Rank](./notebook/Maximal_Network_Rank.md)
* 深度优先 广度优先



十、滑动窗口

* [Subarrays with K Different Integers](./notebook/Subarrays_with_K_Different_Integers.md)
* [字符串的排列](./notebook/字符串的排列.md)



十、其他

* [数组中数字出现的次数](./notebook/数组中数字出现的次数.md)（剑指offer）2020/8/11
* [数组中数字出现的次数Ⅱ](./notebook/数组中数字出现的次数Ⅱ.md)（剑指offer）2020/8/11
* [和为s的两个数字](./notebook/和为s的两个数字.md) 2020/8/17
* [早餐组合](早餐组合.md) 2020/9/12
* [快速公交](快速公交.md) 2020/9/13
* [Linked_List_Cycle](./notebook/Linked_List_Cycle.md) 2020/10/10
* [Linked_List_Cycle_2](./notebook/Linked_List_Cycle_2.md) 2020/10/11
* [Split_Two_Strings_to_Make_Palindrome](./notebook/Split_Two_Strings_to_Make_Palindrome.md) 2020/10/12
* [One Away LCCI](./notebook/One_Away_LCCI.md) 2021/1/26
* [★★ 从给定原材料中找到所有可以做出的菜](./notebook/从给定原材料中找到所有可以做出的菜.md) （Leetcode周赛题目）
* [★★ 判断一个括号字符串是否有效](./notebook/判断一个括号字符串是否有效.md) （Leetcode周赛题目，从左向右遍历找不可修改的右括号数量是否一直大于左括号加可修改的右括号的数量，同理从右向左遍历）
* [★统计特殊四元组](./notebook/统计特殊四元组.md) （用哈希记录`nums[d]-nums[c]`的值的次数，`b`从右向左遍历，每次更新哈希表，然后遍历`a`）
* [★★一手顺子](./notebook/一手顺子.md) （用`unordered_map num2count`记录每个数字的次数，用`priority_queue`构建一个优先队列每次找最小的牌）
* [★位1的个数](./notebook/位1的个数.md) （`n&(n-1)`可以将最低位的1变为0）
* 



二分查找

* [在排序数组中查找数字Ⅰ](./notebook/在排序数组中查找数字Ⅰ.md) （二分法找左右边界）
* [★★★ 最长重复子串](./notebook/最长重复子串.md) （二分法+Rabin-Karp字符串哈希）



背包问题

* [Coin LCCI](./notebook/Coin.md) 2021/2/8



## 面试必备题

重建二叉树（递归与迭代两种方法）

最小K个数（快排思想，手写最小堆）

二叉搜索树的后序遍历序列（递归，单调栈）



## Reference

[1] [labuladong的算法小抄](https://labuladong.gitbook.io/algo/)