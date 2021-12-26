# [842. Split Array into Fibonacci Sequence](https://leetcode-cn.com/problems/split-array-into-fibonacci-sequence/)

**Q:**Given a string `S` of digits, such as `S = "123456579"`, we can split it into a *Fibonacci-like sequence* `[123, 456, 579].`

Formally, a Fibonacci-like sequence is a list `F` of non-negative integers such that:

- `0 <= F[i] <= 2^31 - 1`, (that is, each integer fits a 32-bit signed integer type);
- `F.length >= 3`;
- and` F[i] + F[i+1] = F[i+2] `for all `0 <= i < F.length - 2`.

Also, note that when splitting the string into pieces, each piece must not have extra leading zeroes, except if the piece is the number 0 itself.

Return any Fibonacci-like sequence split from `S`, or return `[]` if it cannot be done.

**Note:**

1. `1 <= S.length <= 200`
2. `S` contains only digits.



## solution1

**Idea**

- i、j、k分别代表第一个、第二个和第三个数字的起始下标，i 初始化为0表示第一个数字的下标包含0
- 数字超过 INT_MAX 直接返回 false
- 回溯的出口为递归到字符串都完成匹配

**Code**

```C++
class Solution {
public:
    vector<int> splitIntoFibonacci(string& S) {
        vector<int> res;
        int i=0;
        for(int j=i+1;j<S.size();++j){
            for(int k=j+1;k<S.size();++k){
                res.clear();
                if(backtrack(S,i,j,k,res)){
                    if(res.size()>2){
                        return res;
                    }
                }
            }
        }
        return {};
    }

    bool backtrack(string& S,int i,int j,int k,vector<int>& res){
        //s[i]、s[j]为'0'，相差一位的话，满足题意
        if((S[i]=='0'&&j-i>1)||(S[j]=='0'&&k-j>1))return false;
        long long a=0,b=0;
        //提取a和b
        for(int c=i;c<j;++c){
            a=a*10+S[c]-'0';
            if(a>INT_MAX)return false;
        }
        for(int c=j;c<k;++c){
            b=b*10+S[c]-'0';
            if(b>INT_MAX)return false;
        }
        //如果达到最后个字符
        if(k==S.size()){
            res.push_back(a);
            res.push_back(b);
            return true;
        }
        //判断第三个数字是否满足条件
        string sum=to_string(a+b);
        for(int c=0;c<sum.size();++c){
            if(S[c+k]!=sum[c])return false;
        }
        res.push_back(a);
        return backtrack(S,j,k,k+sum.size(),res);
    }
};
```



**Complexity Analysis**

* Time Complexity：$O(2^N)$。
* Space Complexity：

