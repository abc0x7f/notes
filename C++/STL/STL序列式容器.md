# vector
`std::vector`是STL提供的**内存连续的可变长度**的数组/列表数据结构.
## 定义
```cpp
#include <vector>
#include <iostream>

int main() {
	std::vector<TYPENAME> VARNAME;
	std::vector<int> a;
	std::vector<int> arr[100];
	std::cout << arr[0];
	return 0;
}
```
**低维是高维的地址**
>输出
>0x61fe00 // arr第1行的地址

另有定义
```cpp
int main() {
	int n = 100, m = 200, v = 5;
	vector<int> arr(n, v);
	// 大小为[0 ~ n - 1],初值为v的arr[i]数组
	vector<vector<int>> p(n, vector<int>(m, v))
	// n * m的二维数组,初值为v
}
```
若想避免多次扩充内存,可使用`reserve(n)`提前预留空间.
```cpp
vector<int> arr; // 创建空vector
arr.reserve(3); // 将arr内容量扩充为至少可容纳三个元素,但并未创建对象
```
vector常用于元素个数不确定的数组,或是实现邻接表.
## 访问
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
	vector<int> arr;
	for (int i = 0; i < 5; i++)
		arr.push_back(i);
	cout << arr[0] << endl;// 数组访问
	
	cout << arr.at(4) << endl; // 返回vector中下标为4的值(同时进行越界检查)
	
	vector<TYPENAME>::iterator VARNAME;
	vector<int>::iterator it;
	it = arr.begin();
	for (int i = 0; i < arr.size(); i++)
		cout << it[i] << endl; //迭代器访问 类似指针
	return 0;
}
```
也可写成
```cpp
vector<int>::iterator it = arr.begin();
for(int i = 0; i < arr.size(); i++)
	cout << *(it + i) << endl;
	//it[i] <=> *(it + i)
```
或者
```cpp
for(auto i = it.begin(); i != it.end(); i++)
	cout << *it << endl;
//类似于遍历字符串
for(int i = 0; str[i] != '\0'; i++)
	cout << str[i] << endl;
```
## 常用函数
### 长度相关
1. `size()`返回元素个数,即`std::distance(v.begin(), v.end())`,复杂度O(1).
2. `empty()`返回是否为空,即`arr.begin() == arr.end()`,复杂度O(1).
3. `arr.resize(n, v)`将容器大小变为n,多余元素用`v`填充,若`v`省略则用默认构造填充.
### 容量相关
1. `reserve(n)`将`arr`内容量扩充为至少可容纳n个元素,但不创建对象(无法引用).
2. `capacity()`返回容器容量上限.
### 元素增删及修改
1. `clear()`清除所有元素,复杂度O(n).
2. `insert()`在vector的指定位置中插入元素.复杂度与距末尾长度线性相关.
 ```cpp
insert(__position,__x);
__position：– A const_iterator into the %vector.
__x:– Data to be inserted.
int main() {
	vector<int> arr = {0, 1, 2, 3};
	arr.write();
	arr.insert(arr.begin() + 2, -1);
	arr.write();
}
```
>输出
> 0 1 2 3
> 0 1 -1 2 3 // a[2]处插入

| 语法格式 | 用法说明 |
| --- | --- |
| `it = a.insert(pos, elem)` | 在迭代器`pos`位置插入值`elem`并返回该位置的迭代器 |
| `it = a.insert(pos, n, elem)` | 在迭代器`pos`位置插入n个元素`elem`并返回该位置的迭代器 |
| `it = a.insert(pos, fir, las)`| 在迭代器`pos`位置插入其他容器(不局限于vector)`[fir, las)`区域的所有元素并返回该位置迭代器 |
| `it = a.insert(pos, {x1, ..., xn})` | 在迭代器`pos`位置插入该初始化列表的元素,并返回该位置的迭代器 |
3. `emplace(__it, __x)`(C++11)在迭代器`__it`处插入值`__x`,仅能插入单个元素但效率更高.
4. `erase()`删除某个迭代器或区间内元素.复杂度与距末尾长度线性相关.
```cpp
erase(__position);
erase(__positionBegin,__positionEnd);
int main() {
	vector<int> a = {0, 1, 2, 3, 4};
	vector<int> b = {0, 1, 2, 3, 4};
	a.erase(a.begin() + 3); a.write();
	b.erase(b.begin() + 1, b.begin() + 3); b.write();
}
```
>输出
>0 1 2 4
>0 4
```cpp
void std::vector<int>::push_back(const int &__x)
void std::vector<int>::pop_back()
```
5. `push_back()`末尾插入元素,`pop_back()`弹出末尾元素,类似于栈.均摊常数复杂度.
6. `a1.swap(a2)`与另一个容器进行交换,复杂度O(1).
### 其他注意事项
1. `vector<bool>`并非stl容器,可用`bitset`代替.
# array (C++11)
stl对原生数组的直接封装,**内存连续长度固定**.
## 定义
```cpp
std::array<int, 3> a0;
std::array<int, 3> b0 = {0, 1, 2};
a0.fill(5);
a0.write(); b0.write();
```
>输出
>5 5 5
>0 1 2
## 访问
| 函数 | 作用 |
| --- | --- |
| `at(pos)` | 访问指定的元素,同时进行越界检查 |
| `operator[]` | 访问指定的元素,**不**进行越界检查 |
| `front()` | 访问第一个元素 |
| `back()` | 访问最后一个元素 |
| `data()` | 返回指向内存中数组第一个元素的指针 |
`at` 若遇 `pos >= size()` 的情况会抛出 `std::out_of_range`.
### 其他函数 (简略)
| 函数 | 作用 |
| --- | --- |
| `operator=` | 以来自另一`array`的每个元素重写`array`的对应元素 |
| `operator==`等 | 按照字典序比较`array`中的值 |
| `std::swap` | 特化的`std::swap`算法 |
# deque
`deque`是STL提供的双端队列数据结构.
## 定义
`deque`的定义及迭代器与`vector`相同,以下不再做介绍.
## 元素访问
| 函数 | 作用 |
| --- | --- |
| `at(pos)` | 访问指定的元素,同时进行越界检查 |
| `operator[]` | 访问指定的元素,**不**进行越界检查 |
| `front()` | 访问第一个元素 |
| `back()` | 访问最后一个元素 |

## 常用函数(简略)
相比`vector`增加了`push_front()`和`pop_front()`两个函数,此外这两个函数与`push_back()`,`pop_back()`时间复杂度都为常数.

# list
`std::list`是STL提供的双向链表数据结构.能够提供**线性**复杂度的随机访问,以及常数复杂度的插入和删除.
## 定义及访问
与`deque`类似(`push_back()`,`push_front()`等),但访问的复杂度不同.
由于`list`的实现是链表,因此它不提供随机访问的接口.若需要访问中间元素，则需要使用迭代器.
`front()`返回首元素的值,`back()`返回末尾元素的值.
## 常用函数 (待完成)
`splice()`,`remove()`,`sort()`,`unique()`,`merge()`.
## forward_list (待完成)