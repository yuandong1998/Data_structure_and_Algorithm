# Heap



## 1. 什么是堆

**优先队列**（priority Queue）：特殊的"队列"，取出元素的顺序是依照元素的优先级（关键字）大小，而不是元素进入队列的先后顺序，以**完全二叉树**存储。

![](https://cdn.mathpix.com/snip/images/Yw3B4bdTPFz7un2Y-tWX0wHZ3tkS_LB31x6zmJTqpMc.original.fullsize.png)



**特性：**

* 结构性：用**数组**表示的**完全二叉树**
* 有序性：任一结点的关键字是其子树所有结点的最大值（或最小值）
  * 最大堆
  * 最小堆



## 2、堆的抽象数据类型描述

- 数据名称：最大堆（MaxHeap）

- 数据对象集：完全二叉树，每个结点的元素值**不小于**其子结点的元素值

- 操作集：最大堆 $H \in MaxHeap$，元素 $item \in ElementType$

  主要操作有：

  - `MaxHeap Create(int MaxSize)`：创建一个空的最大堆
  - `Boolean IsFull(MaxHeap H)`：判断最大堆 H 是否已满
  - `Boolean Insert(MaxHeap H,ElementType item)`：将元素 item 插入最大堆 H
  - `Boolean IsEmpty(MaxHeap H)`：判断最大堆 H 是否为空
  - `ElementType DeleteMax(MaxHeap H)`：返回 H 中最大元素（高优先级）



## 3

### 3.1 插入

插入数组最后一个位置，再从下往上找合适地方



### 3.2 删除

 删除根结点，将数组最后一个位置的数取到根结点，从上往下找合适地方

```C
#include<stdio.h>
#include<malloc.h>
#define MaxData 100000
#define ERROR -1
typedef int ElementType;
typedef struct HeapStruct *MaxHeap;
struct HeapStruct{
	ElementType *Elements;   // 存储堆元素的数组 
	int Size;      // 堆的当前元素个数 
	int Capacity;  // 堆的最大容量 
};

MaxHeap Create(int MaxSize);  // 建堆 
bool IsFull(MaxHeap H);    // 判断堆是否满
bool Insert(MaxHeap H,ElementType item);   // 插入元素
bool IsEmpty(MaxHeap H);    //  判断堆是否为空
ElementType DeleteMax(MaxHeap H);  // 删除并返回堆中最大元素
void LevelOrderTraversal(MaxHeap H);  // 层序遍历 

// 建堆 
MaxHeap Create(int MaxSize){
	MaxHeap H = (MaxHeap)malloc(sizeof(struct HeapStruct));
	// Elements[0] 作为哨兵，堆元素从  Elements[1] 开始存放 
	H->Elements = (ElementType *)malloc((MaxSize+1) * sizeof(ElementType));
	H->Size = 0;
	H->Capacity = MaxSize;
	// "哨兵"大于堆中所有可能的值 
	H->Elements[0] = MaxData;
	return H;
} 

// 插入，从完全二叉树的最后一个位置插入 
bool Insert(MaxHeap H,ElementType item){
	if(IsFull(H)){
		printf("堆已满，无法插入！\n");
		return false;
	}
	int i = ++H->Size;  // 指向堆中最后一个位置 
	for(;H->Elements[i/2] < item;i/=2)    // 向上找比 item 大的结点 
		H->Elements[i] = H->Elements[i/2];  //  向下赋值 
	H->Elements[i] = item;  // 找到了，把 item 值放进去 
	return true;
}

// 删除，从根结点删除 
ElementType DeleteMax(MaxHeap H){
	int parent,child;
	ElementType Max,tmp;
	if(IsEmpty(H)){
		printf("堆为空，无法删除！\n");
		return ERROR;
	}
	Max = H->Elements[1];  // 拿到最大值
	tmp = H->Elements[H->Size--];  // 拿到完全二叉树最后一个值 
	// 判别条件：parent 是否有左孩子结点 
	for(parent=1;parent*2<=H->Size;parent=child){
		// 左右孩子结点中找较大的值 
		child = 2 * parent;  // 左孩子结点 
		// child!=H->Size 表示 child 不为当前最后一个结点，即 parent 有右孩子结点 
		if((child!=H->Size) &&(H->Elements[child] < H->Elements[child+1]))
			child++;  
		// 给 tmp 找个合适的位置 
		// 如果当前左右孩子结点比 tmp 都小，说明 tmp 位置已经合适 
		if(H->Elements[child] <= tmp)
			break;
		else    // 否则把较大的孩子结点提上来，自己继续下去找 
			H->Elements[parent] = H->Elements[child];
	}
	H->Elements[parent] = tmp;  // 在合适的位置把 tmp 放进去 
	return Max;
} 

// 判断是否已经满 
bool IsFull(MaxHeap H){
	return (H->Size == H->Capacity);
}

// 判断是否为空
bool IsEmpty(MaxHeap H){
	return !H->Size;
}

// 层序遍历
void LevelOrderTraversal(MaxHeap H){
	int i;
	printf("层序遍历的结果是：");
	for(i = 1;i<=H->Size;i++){
		printf("%d ",H->Elements[i]);
	} 
	printf("\n"); 
} 

int main(){
	MaxHeap H;
	int MaxSize = 100;
	H = Create(MaxSize);
	Insert(H,55);
	Insert(H,66);
	Insert(H,44);
	Insert(H,33);
	Insert(H,11);
	Insert(H,22);
	Insert(H,88);
	Insert(H,99);
	/*
		 99
		/  \
	   88  66
	  / \  / \
	 55 11 22 44
	/ 
   33	  
	*/
	LevelOrderTraversal(H);
	DeleteMax(H);
	LevelOrderTraversal(H);
	DeleteMax(H);
	LevelOrderTraversal(H);
	DeleteMax(H);
	LevelOrderTraversal(H);
	DeleteMax(H);
	LevelOrderTraversal(H);
	return 0;
}
```

