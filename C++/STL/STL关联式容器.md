# set
内部有序,**不含重复元素**(可用于去重).若需含相同元素的集合可使用`multiset`.
## 定义
```cpp
#include <set>
#include <iostream>

int main() {
	set<TYPENAME> VARNAME;
	set<int> a; //单set
	set<int> s[SIZE]; //set数组
}
```
## 访问
**set内元素只能通过迭代器(iterator)访问**
```cpp
set<int>::iterator it;
it = s.begin();
```
此时可以通过`*it`访问set内元素.
注意除了序列式容器以外都不支持`*(it+i)`的访问方式.
```cpp
for(auto it = s.begin(); it != s.end(); it++)
	cout << *it << endl;
```
## 常用函数
### 增删操作
1. `insert(x)`当容器内没有值为`x`的元素时插入元素.
```cpp
set<char> s;
s.insert('A');
```
2. `erase(x)`删除值为`x`的所有元素,删除单个元素时有迭代器和值两种方式:

迭代器**不能**指向`set`以外元素(如`end()`),复杂度为$O(1)$.
值可以为任意值(若未找到则不产生影响),复杂度为$O(logn)$.
```cpp
set<int> s; 
auto it = s.begin();
s.erase(it); //删除迭代器所指元素
s.erase(100); //删除值为100的元素
```
删除区间元素可以用`s.erase(iteratorBegin , iteratorEnd)`.
`iteratorEnd`为所需要删除区间的结束迭代器的下一个地址.
即范围为`[iteratorBegin,iteratorEnd)`.
```cpp
set<int> s;
for(int i = 0; i < 10; i++) s.insert(i);
auto it = s.find(5);
s.erase(it, s.end());
s.write();
```
>结果
>0 1 2 3 4
### 查找操作
1. `find(x)`返回值`x`所对应的**迭代器**,如果未找到对应值则返回`end()`.
```cpp
set<int> s;
for(int i = 1; i <= 3; i++) s.insert(i + 10);
set<int>::iterator it = s.find(12);
cout << *it << " " << *(s.find(13)) << endl;
```
>输出
>12 13

2. `count(x)`返回`set`内值为`x`的元素数量.
3. `lower_bound(x)`返回指向首个不小于值`x`的迭代器.如果不存在这样的元素则返回`end()`.
4. `upper_bound(x)`返回指向首个大于值`x`的迭代器.如果不存在这样的元素则返回`end()`.
>`set`自带的`lower_bound()`和`upper_bound()`的时间复杂度为$O(logn)$.
>但使用`algorithm`库中的`lower_bound`和`upper_bound`函数对`set`中的元素进行查询,时间复杂度为$O(n)$.
>`set`没有提供自带的`nth_element`.使用`algorithm`库中的`nth_element`查找第$k$大的元素时间复杂度为$O(n)$.
>如果需要实现平衡二叉树所具备的$O(logn)$查找第$k$大元素的功能,需使用`pb_ds`库中的平衡二叉树.

5. `empty()`返回容器是否为空,复杂度$O(1)$.
6. `size()`返回容器内元素个数,复杂度$O(1)$.

# map
`map`是有序键值对容器,它的元素的键是唯一的.搜索,移除和插入操作拥有对数复杂度.
## 定义
`map`重载了`operator[]`可以用任意定义了`operator <`的类型作为下标(在`map`中叫做`key`,也就是索引):
```cpp
map<Key, T> yourMap;
map<string, int> mp = {{"TOM", 100}, {"LUCY", 98}}; // mp["TOM"] = 100;
```
其中,`Key`是键的类型,`T`是值的类型.
## 访问
1. 直接通过下标进行访问.
2. 通过迭代器进行访问,迭代器的引用值为`pair<Key, T>`的键值对.
```cpp
map<string, int> mp;
for (auto it = mp.begin(); it != mp.end(); it++)
	cout << (*it).first << " " << (*it).second << endl;
```
或是:
```cpp
for (auto it : x) it.write(); 
```

## 常用函数
### 增删操作
1. 可以直接通过下标访问来进行查询和插入,如: 
```cpp
mp["TOM"] = 100;
cout << mp["TOM"] << endl;
```
>当下标访问某个元素时,若`map`中不存在对应键值的元素,则会自动插入一个值为默认值的新元素.此操作过于频繁时会影响`map`的效率.因此一般情况下推荐使用`find()`寻找特定键的元素.

2. 通过向`map`中插入一个类型为`pair<Key, T>`的值可以达到插入元素的目的,例如`mp.insert(pair<string,int>("Alan",100));`.
3. `erase(key)`会删除**所有**键为`key`的元素,返回值为删除元素的数量.
4. `erase(it)`删除迭代器为`it`的元素,要求迭代器必须合法.
5. `erase(first,last)`: 删除迭代器在$[fir,las)$范围内的所有元素.
6. `clear()`清空整个容器.

### 查询操作
| 函数 | 作用 |
| --- | --- |
| `count(x)` | 返回容器内键为`x`的元素数量.复杂度为$O(\log(size)+ans)$ (关于容器大小对数复杂度，加上匹配个数).|
| `find(x)` | 若容器内存在键为`x`的元素,会返回该元素的迭代器,否则返回`end()`. |
| `lower_bound(x)` | 返回指向首个不小于给定键的元素的迭代器.若容器内所有元素均小于给定键,返回`end()`. |
| `upper_bound(x)` | 返回指向首个大于给定键的元素的迭代器.若容器内所有元素均小于或等于给定键,返回`end()`.
| `empty()` | 返回容器是否为空. |
| `size()` | 返回容器内元素个数. |

# 自定义比较方式 (待补充)
`set`在默认情况下的比较函数为`<`(如果是非内置类型需要重载`<`运算符).然而在某些特殊情况下,我们希望能自定义`set`内部的比较方式.
具体来说,我们需要定义一个类,并在这个类中重载`()`运算符.
```cpp
struct cmp {
	bool operator ()(int a, int b) const {
		return a > b;
	}
};
set<int, cmp> s;
```
