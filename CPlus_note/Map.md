# Map 

C++中的map分为`map`和`unorder_map`

[TOC]



## 查找 find

find() 函数返回一个迭代器指向键值为 key 的元素，如果没找到就返回指向 map 尾部的迭代器。判断是否找到采用`map.find(c) == map.end()`