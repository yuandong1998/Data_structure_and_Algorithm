# Lec07哈希表

## 1. Symbol-table problem

<img src="https://i.bmp.ovh/imgs/2021/03/f477d74188917789.png" style="zoom:67%;" />

## 1. Direct-access tables

IDEA:假设keys来自集合$U\in\{0,1,...,m-1\}$，并且keys都是distinct的。创建一个数组$T[0,...,m-1]$。

<img src="https://i.bmp.ovh/imgs/2021/03/f0493f6664f6a4fe.png" style="zoom:50%;" />

operations的worst-time为$\Theta(1)$



**hash and collision**

Hashing:Hash function h maps keys "randomly" into slots of table T.

When a record to be inserted maps to an already occupied slot in T, a collision occurs.



 ## 2. Resolving collisions by chaining

**IDEA:**Link records in the same slot into a list

**worst case:**Every key hashes to the same slot. Access time:$\Theta(n)$

**Average-case:** We make the assumption of simple uniform hashing. `n` be the number of keys in the table, and let `m` be the number of slots.$\alpha=n/m$ average number of keys per slot.

*  unsuccessful search:$\Theta(1+\alpha)$. (apply hash function and access slot+search the list)

* A successful search has same asymptotic bound. 证明难，见书本.

  

## 3. Choosing hash functions

均匀分布很难保证，好的hash函数应该满足以下条件

* 尽量均匀分布
* keys的规律性不影响均匀性



**Division method**

Assume all keys are integers, and define $h(k)=k\ mod\ m$.

缺点：不要选取有小divisor d的m，回影响分布均匀。if $m=2^r$，then the hash doesn’t even depend on all the bits of k.

Pick m to be a prime not too close to a power of 2 or 10.但是table size设置为质数不方便。

除法在计算机比较慢。



**Multiplication method**

Assume that all keys are integers, $m = 2^r$, and our computer has `w-bit` words. Define $h(k)=(A*k\ mod2^w)rsh(w-r)$,where `rsh` is the “bitwise right-shift” operator and A is an odd integer in the range $2^{w–1} < A < 2^w$.

* Don’t pick A too close to $2^{w–1}$ or $2^w$.
* 比除法快
* rsh也快

![](https://i.bmp.ovh/imgs/2021/03/c284d9544692182d.png)





## 4. Resolving collisions by open addressing 开放寻址

- no storage for link.
- Insertion systematically probes the table until an empty slot is found.
- The hash function depends on both the **key** and **probe number**
- The probe sequence 〈h(k,0), h(k,1), …, h(k,m–1)〉 should be a permutation of {0, 1, …, m–1}.
- The table may fill up, and deletion is difficult (but not impossible). 因为删除一个key后可能会影响其他key的搜索。

Search uses the same probe sequence, terminating successfully if it finds the key and unsuccessfully if it encounters an empty slot.搜索使用相同的探针序列，如果找到密钥，则成功终止，如果遇到空插槽则不成功。



### 4.1 Probing strategiesProbing strategies

**1. Linear probing：** $h(k,i) = (h′(k) + i) mod m$，这种方法虽然简单，但受到主聚类（primary clustering）的影响，其中长期占用的插槽会积聚起来，从而增加平均搜索时间。此外，长期占用的插槽往往变长。通常结合**Multiplication method**使用。



**2. Double hashing：** $h(k,i) = (h_1(k) + i⋅ h_2(k))\ mod\ m$ 

This method generally produces excellent results, but $h_2(k)$ must be relatively prime to m. One way is to make m a power of 2 and design $h_2(k)$ to produce only odd numbers.



### 4.2 Analysis of open addressing

We make the assumption of uniform hashing:  Each key is equally likely to have any one of the m! permutations as its probe sequence.

**Theorem.** Given an open-addressed hash table with load factor$ α = n/m < 1$, the expected number of probes in an unsuccessful search is at most $1/(1–α)$.

**Proof** 

* At least one probe is always necessary
* With probability n/m, the first probe hits an occupied slot, and a second probe is necessary
* With probability (n–1)/(m–1), the second probe hits an occupied slot, and a third probe is necessary. 
* With probability (n–2)/(m–2), the third probe hits an occupied slot, etc

可以看出：$\frac{n-i}{m-i}<\frac{n}{m}=\alpha \text { for } i=1,2, \ldots, n$

<img src="https://cdn.mathpix.com/snip/images/EsuHCuh28rYDn2otEfxj2Bi5H-N7phYvrU1gf9aJNUY.original.fullsize.png" style="zoom:50%;" />



* If α is constant, then accessing an openaddressed hash table takes constant time.
* If the table is half full, then the expected number of probes is 1/(1–0.5) = 2
* If the table is 90% full, then the expected number of probes is 1/(1–0.9) = 10.
* 随着越来越满，速度越来越慢。

