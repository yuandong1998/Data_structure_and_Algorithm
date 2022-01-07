# String 字符串

掌握基本的C++STL字符串操作，达到刷题水平即可

[TOC]

**TODO LIST**

[ ] atoi

[ ] c_str

[ ] find

[ ] size_t





## 1. 字符串切片

**substr**

`string substr (size_t pos = 0, size_t len = npos) const;`

从`pos`位置开始向后`len`个字符，构建一个新的字符串对象，如果`len`省略则到字符串末尾。



## 2. 字符串转数字

**stoi**

`int stoi (const string&  str, size_t* idx = 0, int base = 10);`

idx是`size_t`类型的指针，函数设置为 str 中数值后的下一个字符的位置。也就是如果`str=123abc`，idx是指向`a`的指针。

base是表示字符串的进制，如果base是 0，则使用的基数由序列中的格式决定。



**atoi**



## 3. 字符串查找

**find**

```
size_t find (const string& str, size_t pos = 0) const noexcept; //string (1)	
size_t find (const char* s, size_t pos = 0) const; //c-string (2)	
size_t find (const char* s, size_t pos, size_type n) const; //buffer (3)
size_t find (char c, size_t pos = 0) const noexcept; //character (4)
```

从字符串pos位置开始找`str`，也可以找字符`c`，返回第一次出现的位置，如果没找到返回`string::npos`。`n`是指匹配`s`中的长度，就是只查找s[0~n-1]的部分。



**rfind**

**find_first_of**

**find_last_of**

**find_first_not_of**

**find_last_not_of**



## 4. 字符串按照长度排序

```C++
sort(words.begin(), words.end(), [&](const string & a, const string & b){
            return a.size() < b.size(); 
});
```



## 5. 字符串split

```C++
auto split = [](const string& s, char delim) -> vector<string> {
    vector<string> ans;
    string cur;
    for (char ch: s) {
        if (ch == delim) {
            ans.push_back(move(cur));
            cur.clear();
        }
        else {
            cur += ch;
        }
    }
    ans.push_back(move(cur));
    return ans;
};
```

