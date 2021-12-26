# [求和路径](https://leetcode-cn.com/problems/paths-with-sum-lcci/)

Question

![](https://i.bmp.ovh/imgs/2021/02/790b692eafc3fa57.png)



## Method1

**Idea**

DFS，从每个节点进行DFS。



**Code**

```C++
class Solution {
public:
    int res=0;
    int pathSum(TreeNode* root, int sum) {
        if(!root){return 0;}
        dfs(root,sum);
        pathSum(root->left,sum);
        pathSum(root->right,sum);
        return res;
    }
    void dfs(const TreeNode* root,const int target){
        if(!root){
            return;
        }
        if(root->val==target){
            res++;
        }
        dfs(root->left,target-root->val);
        dfs(root->right,target-root->val);
    }
};

```



## Method2

**Idea**

前缀和+DFS，用数组记录前缀和，presum[i]-presum[j]表示从i到j的和，采用回溯的方法求解。



**Code**

```C++
class Solution {
public:
    int res;
    void backtrack(TreeNode* root,vector<int>& presum,int target,int len){
        if(!root) return;
        presum.push_back(presum.back()+root->val);
        for(int i=0;i<len;i++){
            if(presum.back()-presum[i]==target) res++;
        }
        backtrack(root->left,presum,target,len+1);
        if(root->left) presum.pop_back();

        backtrack(root->right,presum,target,len+1);
        if(root->right) presum.pop_back();
    }
    int pathSum(TreeNode* root, int sum) {
        res=0;
        vector<int> presum;
        presum.push_back(0);
        backtrack(root,presum,sum,1);
        return res;
    }
};
```

