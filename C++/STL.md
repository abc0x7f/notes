# 1.容器 (Containers)
## 1.1 vector
### 定义
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
输出为
```
0x61fe00 //arr第1行的地址
```
另有定义
```cpp
int main() {
	int n = 100, m = 200, v = 5;
	vector<int> arr(n, v);
	//大小为[0 ~ n - 1],初值为v的arr[i]数组
	vector<vector<int>> p(n, vector<int>(m, v))
	//n * m的二维数组,初值为v
}
```
vector常用于元素个数不确定的数组,或是实现邻接表
### 访问
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
	//数组访问
	vector<int> arr;
	for(int i = 0; i < 5; i ++)
		vector.push_back(i);
	cout << arr[0] << endl;
	//迭代器访问 类似指针
	vector<TYPENAME>::iterator VARNAME;
	vector<int>::iterator it;
	it = arr.begin();
	for(int i = 0; i < arr.size(); i ++)
		cout << it[i] << endl;
	return 0;
}
```
也可写成
```cpp
vector<int>::iterator it = arr.begin();
for(int i = 0; i < arr.size(); i ++)
	cout << *(it + i) << endl;
	//it[i] <=> *(it + i)
```
或者
```cpp
for(auto i = it.begin(); i != it.end(); i ++)
	cout << *it << endl;
//类似于遍历字符串
for(int i = 0; str[i] != '\0'; i ++)
	cout << str[i] << endl;
```
### 常用函数
#### push_back()与pop_back()
push_back()末尾插入元素,pop_back()弹出末尾元素,类似于栈
```cpp
void std::vector<int>::push_back(const int &__x)
void std::vector<int>::pop_back()
```
#### size()
返回元素个数,复杂度为O(1)
#### clear()
清空vector中所有元素,复杂度为O(n)
#### insert()
在vector的指定位置中插入元素
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
输出
```
0 1 2 3
0 1 -1 2 3 //a[2]处插入
```
#### erase()
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
输出
```cpp
0 1 2 4
0 4
```
## set
内部有序,不含重复元素(可去重)
### 定义
```cpp
#include <set>
#include <iostream>

int main() {
	set<TYPENAME> VARNAME;
	set<int> a; //单set
	set<int> s[SIZE]; //set数组
}
```
### 访问
**set内元素只能通过迭代器(iterator)访问**
```cpp
set<int>::iterator it;
it = s.begin();
```
此时可以通过\*it访问set内元素
注意除了vector和string之外的STL容器都不支持*(it+i)的访问方式
```cpp
for(auto it = s.begin(); it != s.end(); it ++)
	cout << *it << endl;
```
### 常用函数
#### insert()
插入元素
```cpp
set<char> s;
s.insert('A');
```
#### find()
**find(value)返回的是set中value所对应的迭代器，也就是value的指针(地址)**
如果未找到对应值的元素则返回end()
```cpp
set<int> s;
for(int i = 1; i <= 3; i ++) s.insert(i + 10);
set<int>::iterator it = s.find(12);
cout << *it << " " << *(s.find(13)) << endl;
```
输出
```cpp
12 13
```
#### erase()
删除单个元素时有迭代器和值两种方式
迭代器不能指向set以外元素(如end()),复杂度为O(1)
值可以为任意值(若未找到则不产生影响),复杂度为O(logn)
```cpp
set<int> s; 
auto it = s.begin();
s.erase(it); //删除迭代器所指元素
s.erase(100); //删除值为100的元素
```
删除区间元素可以用st.erase(iteratorBegin , iteratorEnd)
**iteratorEnd**为所需要删除区间的结束迭代器的下一个地址
即范围为\[iteratorBegin,iteratorEnd\)
```cpp
set<int> s;
for(int i = 0; i < 10; i ++) s.insert(i);
auto it = s.find(5);
s.erase(it, s.end());
s.write();
```
结果
```cpp
0 1 2 3 4
```
#### size()
返回元素个数,复杂度为O(1)