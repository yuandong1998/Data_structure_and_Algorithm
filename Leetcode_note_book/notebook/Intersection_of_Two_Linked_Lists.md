# [链表相交](https://leetcode-cn.com/problems/intersection-of-two-linked-lists-lcci/)

Question

<img src="https://i.bmp.ovh/imgs/2021/01/57596395eca92142.png" style="zoom:67%;" />



## Method 1

**IEDA**

设链表A的长度为a，链表B的长度为b，A到相交结点的距离为c,B到相交节点的距离为d，显然可以得到两者相交链表的长度：a - c = b - d， 变换一下式子得到:a + d = b + c
我们用一个指针从链表A出发，到末尾后就从B出发，用另一个指针从B出发，到末尾后从A出发，由于上面的公式，当前一个指针走了a+d步数时，后一个指针走了b+c,两步数相等，即走到了相交节点。



**CODE**

```C++
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode* h1=headA;
        ListNode* h2=headB;
        while(h1!=h2){
            h1 = h1 == NULL ? headB : h1->next;
            h2 = h2 == NULL ? headA : h2->next;
        }
        return h1;
    }
};
```



**Complexity Analysis:**

* Time Complexity : $O(M+N)$
* Space Complexity : $O(1)$



## Reference

[1] [超简单证明双指针的正确性 - 链表相交 - 力扣（LeetCode） (leetcode-cn.com)](https://leetcode-cn.com/problems/intersection-of-two-linked-lists-lcci/solution/chao-jian-dan-zheng-ming-shuang-zhi-zhen-de-zheng-/)

