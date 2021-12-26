# priority_queue 优先队列

## 1. class template

`template <class T, class Container = vector<T>,class Compare = less<typename Container::value_type> > class priority_queue;`

T表示存的元素的数据类型，`Container`表示存元素用的容器，一般采用`vector`，`Compare`来表示比较关系，采用大根堆还是小根堆。

 

## 2. Priority queue

优先队列是一种容器适配器，根据某种严格的弱排序标准，它的第一个元素总是它所包含的元素中最大的。这个类似于堆，在堆中可以随时插入元素，并且只能检索堆中最大的元素(优先级队列中最顶端的那个)。优先队列是作为容器适配器实现的，它是使用特定容器类的封装对象作为其基础容器的类，提供一组特定的成员函数来访问其元素。元素是从特定容器的后面弹出的，该容器称为优先级队列的顶部。基础容器可以是任何标准容器类模板，也可以是其他一些特别设计的容器类。容器应该可以通过[随机访问迭代器](http:www.cplusplus.comRandomAccessIterator)访问，并支持以下操作：

- `empty()`
- `size()`
- `front()`
- `push_back()`
- `pop_back()`
- `emplace()`



标准容器类`vector`和`deque`满足这些要求。默认情况下，如果没有为特定优先级队列类实例化指定容器类，则使用标准容器`vector`。为了在内部始终保持堆结构，需要支持随机访问迭代器。这是由容器适配器通过在需要时自动调用算法函数`make_heap`、`push_heap`和`pop_heap`自动完成的。



### 3. Template parameters

* **T** ：Type of the elements.

* **Container** ：存储元素的内部基础容器对象的类型。其value_type应为T。

* **Compare** ：一个以两个元素（类型为T）作为参数并返回布尔值的二进制谓词，默认为 `less<T>`。

  

如果不写后两个参数，那么容器默认用的是vector，比较方式默认用operator<，也就是优先队列是大顶堆，队头元素最大。



## Member functions

- [**(constructor)**](http://www.cplusplus.com/reference/queue/priority_queue/priority_queue/)：Construct priority queue (public member function )

- [**empty**](http://www.cplusplus.com/reference/queue/priority_queue/empty/)：Test whether container is empty (public member function )

- [**size**](http://www.cplusplus.com/reference/queue/priority_queue/size/)：Return size (public member function )

- [**top**](http://www.cplusplus.com/reference/queue/priority_queue/top/)：Access top element (public member function )

- [**push**](http://www.cplusplus.com/reference/queue/priority_queue/push/)：Insert element (public member function )

- [**emplace** ](http://www.cplusplus.com/reference/queue/priority_queue/emplace/)：Construct and insert element (public member function )

- [**pop**](http://www.cplusplus.com/reference/queue/priority_queue/pop/)：Remove top element (public member function )

- [**swap** ](http://www.cplusplus.com/reference/queue/priority_queue/swap/)：Swap contents (public member function )



## Example

自定义优先级，重载默认的 < 符号

```C++
#include<iostream>
#include<queue>
#include<cstdlib>
using namespace std;
struct Node{
	int x,y;
	Node(int a=0, int b=0):
		x(a), y(b) {}
};
 
struct cmp{
	bool operator()(Node a, Node b){
		if(a.x == b.x)	return a.y>b.y;
		return a.x>b.x;
	}
};
 
int main(){
	priority_queue<Node, vector<Node>, cmp>p;
	
	for(int i=0; i<10; ++i)
		p.push(Node(rand(), rand()));
		
	while(!p.empty()){
		cout<<p.top().x<<' '<<p.top().y<<endl;
		p.pop();
	}//while
	//getchar();
	return 0;
}
```



```C++
//小根堆
priority_queue<int, vector<int>, greater<int> > minheap;
//大根堆
priority_queue<int, vector<int>, less<int> > maxheap;
```

