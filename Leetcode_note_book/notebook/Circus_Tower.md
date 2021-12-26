#### [面试题 17.08. Circus Tower LCCI](https://leetcode-cn.com/problems/circus-tower-lcci/)

Question

![](https://i.bmp.ovh/imgs/2021/04/f1edbfc2ff249ecf.png)



## Method

**IDEA**

动态规划。将身高进行排序后，可以转换为最长上升子序列问题。但要注意多组身高相同但是体重不同的情况。所以对身高进行升序排序，若身高相同对体重进行降序排序，则转为最长上升子序列问题。

用`d[i]`表示长度为`i`的最长上升子序列中的最后的元素。状态转移过程如下：

```
d={};//开始是空序列
for(i in [0,N-1]){
    it = lower_bound(d,d.end,A[i]);
    if(没找到){
        A[i]入d;
    }else{
        d[it] = A[i];
    }
}
```



**code**

代码参考了[Leetcode题解](https://leetcode-cn.com/problems/circus-tower-lcci/solution/dong-tai-gui-hua-by-jason-2-u0r0/)。

```C++
struct cmp2{
    bool operator()(const pair<int,int>& p1,const pair<int,int>& p2)const{
        return p1.first < p2.first || p1.first == p2.first && (p1.second > p2.second);
    }
};
class Solution {
public:
    int bestSeqAtIndex(vector<int>& height, vector<int>& weight) {
        const int N = height.size();
        vector<pair<int,int>> P(N);
        for(int i=0;i<N;++i){
            P[i] = {height[i], weight[i]};
        }
        sort(P.begin(),P.end(),cmp2());
        vector<int> d;
        for(int i=0;i<N;++i){
            auto it = lower_bound(d.begin(),d.end(),P[i].second);
            if(it == d.end()){
                d.push_back(P[i].second);
            }else{
                *it = P[i].second;
            }
        }
        return d.size();
    }
};
```







## Reference

[1] [题目](https://leetcode-cn.com/problems/circus-tower-lcci/)

[2] [Leetcode题解](https://leetcode-cn.com/problems/circus-tower-lcci/solution/dong-tai-gui-hua-by-jason-2-u0r0/)

