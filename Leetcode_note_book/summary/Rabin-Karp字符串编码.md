# Rabin-Karp 字符串编码

$O(N)$时间复杂度的字符串匹配算法



**问题：** 对于长度为`n`的字符串`str`,找是否有子串和字符串长度为`m`的字符串`sub`匹配，比如`str="abcabee",sub="ca"`。

**思想：** 先对`sub`进行哈希得到`hash(sub)`，再从字符串`str`的起始位置开始取长度`m`的子串进行哈希判断是否和`hash(sub)`相等，如果相等则匹配，否则向后移动一位（滑动窗口）。

**具体实现：** 对于字符串`sub`，选择一个质数p，可以将字符串转化为$hash_{sub}=sub[0]*p^{m-1}+sub[1]*p^{m-2},...,+sub[m-1]$。而在滑动窗口进行哈希时不需要每次重新计算一次，相当于左移一位然后去掉最高位，加上新的一位。$hash=hash*p-p^{m}(s[i-m])+s[i]$。最终hash值可能会溢出，所以需要对值取模，但这样可能会导致hash冲突。（unsigned long long 存储相当于自动取模）



## Reference

[1] [Rabin-Karp 演算法的詳細解析 – 拿鐵派的馬克 Blog (mark-lin.com)](https://mark-lin.com/posts/20200625/)

[2] [【微扰理论】Rabin-Karp + 二分搜索 - 最长重复子串 - 力扣（LeetCode） (leetcode-cn.com)](https://leetcode-cn.com/problems/longest-duplicate-substring/solution/wei-rao-li-lun-rabin-karp-er-fen-sou-suo-3c22/)

