# [K 个不同整数的子数组](https://leetcode-cn.com/problems/subarrays-with-k-different-integers/)

Question

![](https://i.bmp.ovh/imgs/2021/02/24b026b6157a5241.png)



## Method1

**Idea**

滑动窗口。对于任一一个右端点，可能存在一系列左端点与其对应，满足两端点所指区间对应的子数组内恰有K个不同整数。通过分析可以发现对于任意一个右端点，能够与其对应的左端点们必然相邻。当右端点右移时候，左端点同样右移或者不动。

采用滑动窗口来解，记录两个左指针left1和left2，来表示左端点区间[left1,left2)，第一个左指针表示极大的包含 K 个不同整数的区间的左端点，第二个左指针则表示极大的包含 K-1 个不同整数的区间的左端点。

**Code**

```C++
class Solution {
public:
    int subarraysWithKDistinct(vector<int>& A, int K) {
        int n = A.size();
        vector<int> num1(n + 1), num2(n + 1);
        int tot1 = 0, tot2 = 0;
        int left1 = 0, left2 = 0, right = 0;
        int ret = 0;
        while (right < n) {
            if (!num1[A[right]]) {
                tot1++;
            }
            num1[A[right]]++;
            if (!num2[A[right]]) {
                tot2++;
            }
            num2[A[right]]++;
            while (tot1 > K) {
                num1[A[left1]]--;
                if (!num1[A[left1]]) {
                    tot1--;
                }
                left1++;
            }
            while (tot2 > K - 1) {
                num2[A[left2]]--;
                if (!num2[A[left2]]) {
                    tot2--;
                }
                left2++;
            }
            ret += left2 - left1;
            right++;
        }
        return ret;
    }
};
```



**Complexity Analysis**

* Time complexity：$O(N)$
* Space complexity：$O(N)$



## Reference

[1] [K 个不同整数的子数组](https://leetcode-cn.com/problems/subarrays-with-k-different-integers/solution/k-ge-bu-tong-zheng-shu-de-zi-shu-zu-by-l-9ylo/)

[2] [K 个不同整数的子数组](https://leetcode-cn.com/problems/subarrays-with-k-different-integers/solution/k-ge-bu-tong-zheng-shu-de-zi-shu-zu-by-l-ud34/)