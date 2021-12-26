# functional中的比较函数

都是头文件`<functional>`的函数，可以配合`sort,merge,lower_bound`等使用。





## 1. greater

```C++
template <class T> struct greater {
  bool operator() (const T& x, const T& y) const {return x>y;}
  typedef T first_argument_type;
  typedef T second_argument_type;
  typedef bool result_type;
};
```

