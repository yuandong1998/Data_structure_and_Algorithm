# [面试题 08.11. 硬币](https://leetcode-cn.com/problems/coin-lcci/)

Question

![](https://i.bmp.ovh/imgs/2021/02/53f80f0b5907d6af.png)



## Method 1

**Idea**

动态规划。

用$f(i,v)$表示前`i`种面值的硬币构成面值为`v`的方案数量，$c_i$表示第`i`种面值的硬币的面值。可得$f(i, v)=\sum_{j=0}^{k} f(i-1, v-j \times c i), k=\left\lfloor\frac{v}{c_{i}}\right\rfloor$，

$f(i, v)=f(i-1, v)+f\left(i-1, v-c_{i}\right)+f\left(i-1, v-2 c_{i}\right) \cdots f\left(i-1, v-k c_{i}\right)$

$f(i, v-c i)=f\left(i-1, v-c_{i}\right)+f\left(i-1, v-2 c_{i}\right)+f\left(i-1, v-3 c_{i}\right) \cdots f\left(i-1, v-k c_{i}\right)$

最终可得$f(i, v)=f(i-1, v)+f(i, v-c i)$

在进一步优化空间复杂度。



**Code**

```C++
class Solution {
private:
    static constexpr int mod = 1000000007;
    static constexpr int coins[4] = {25, 10, 5, 1};

public:
    int waysToChange(int n) {
        vector<int> f(n + 1);
        f[0] = 1;
        for (int c = 0; c < 4; ++c) {
            int coin = coins[c];
            for (int i = coin; i <= n; ++i) {
                f[i] = (f[i] + f[i - coin]) % mod;
            }
        }
        return f[n];
    }
};
```



**Complexity Analysis**

* Time complexity:$O(n)$
* Space complexity:$O(n)$



## Reference

[1] [硬币](https://leetcode-cn.com/problems/coin-lcci/solution/ying-bi-by-leetcode-solution/)