# [BST Sequences LCCI](https://leetcode-cn.com/problems/bst-sequences-lcci/)

**Question**

![](https://i.bmp.ovh/imgs/2021/02/88f994004cb6229b.png)



## Method1

**IDEA**

采用回溯算法与deque，双向队列。每次确定`dq`的size大小再遍历选择列表。



**Code**

```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
vector<int> path;
vector<vector<int>> res;
vector<vector<int>> BSTSequences(TreeNode* root) {
    if (!root) return {{}};
    deque<TreeNode*> dq;
    dq.push_back(root);
    dfs(dq);
    return res;
}
void dfs(deque<TreeNode*>& dq) {
    // base case
    if (dq.empty()) {
        res.push_back(path);
        return;
    }
    int size = dq.size();
    for (int i = 0; i < size; i++) {
        //do action
        TreeNode* node = dq.front();
        dq.pop_front();
        path.push_back(node -> val);

        // 将当前节点的子节点加入选择节点
        if (node -> left) dq.push_back(node -> left);
        if (node -> right) dq.push_back(node -> right);

        // 下一轮递归
        dfs(dq);

        // 回溯选择列表
        // 把加入的子节点pop出后，还要将当前节点重新加入选择列表
        if (node -> left) dq.pop_back();
        if (node -> right) dq.pop_back();
        dq.push_back(node);
        path.pop_back();
    }
}
};
```

