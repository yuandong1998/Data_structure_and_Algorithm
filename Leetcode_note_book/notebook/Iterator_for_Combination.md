# [1286. Iterator for Combination](https://leetcode-cn.com/problems/iterator-for-combination/)



**Q:** Design an Iterator class, which has:

* A constructor that takes a string `characters` of **sorted distinct** lowercase English letters and a number `combinationLength` as arguments.
* A function `next()` that returns the next combination of length `combinationLength` in lexicographical order.
* A function `hasNext()` that returns True if and only if there exists a next combination.



## Solution1

**Idea:**

初始字符串是前`combinationLength`长度的子串，然后最后一个位置不断向后移，直到最后。然后倒数第二个位置向前移一位，最后一个位置回到倒数第二个位置的前一位，再一直向后移动，直到最后。然后不断循环。

通过`pos`数组标记当前字符串的位置，如下代码找到当前需要移动的是第`i`个位置。

```C++
for (int k = pos.size() - 1; k >= 0; --k) {
    if (pos[k] != s.size() - pos.size() + k) {
        i = k;
        break;
    }
}
```

如下代码，移动第`i`个位置，然后将`i`后面的位置回位。

```C+=
else {
	++pos[i];
	for (int j = i + 1; j < pos.size(); ++j) {
		pos[j] = pos[j - 1] + 1;
	}
}
```

这种生成方法的优势在于，我们仅根据当前的组合就可以快速地得到下一个组合，而不需要提前将所有的组合存储在数据结构中。



**Code:**

```C++
class CombinationIterator {
private:
    vector<int> pos;
    string s;
    bool finished;

public:
    CombinationIterator(string characters, int combinationLength) {
        s = characters;
        for(int i=0;i<combinationLength;i++){
            pos.push_back(i);
        }
        //pos.resize(combinationLength);
        //iota(pos.begin(), pos.end(), 0);
        finished = false;
    }
    
    string next() {
        string ans;
        for (int p: pos) {
            ans += s[p];
        }
        int i = -1;
        for (int k = pos.size() - 1; k >= 0; --k) {
            if (pos[k] != s.size() - pos.size() + k) {
                i = k;
                break;
            }
        }
        if (i == -1) {
            finished = true;
        }
        else {
            ++pos[i];
            for (int j = i + 1; j < pos.size(); ++j) {
                pos[j] = pos[j - 1] + 1;
            }
        }
        return ans;
    }
    
    bool hasNext() {
        return !finished;
    }
};

/**
 * Your CombinationIterator object will be instantiated and called as such:
 * CombinationIterator* obj = new CombinationIterator(characters, combinationLength);
 * string param_1 = obj->next();
 * bool param_2 = obj->hasNext();
 */
```



**Complexity Analysis:**

* Time Complexity : `next`的时间复杂度是$O(K)$，`hastNext()`的时间复杂度是$O(1)$
* Space Complexity : $O(1)$



## Reference

[1] [Leetcode官方题解](https://leetcode-cn.com/problems/iterator-for-combination/solution/zi-mu-zu-he-die-dai-qi-by-leetcode-solution/)