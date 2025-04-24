# 栈
STL栈`std::stack`是一种**后进先出**的容器适配器,仅支持查询或删除栈顶元素,不支持随机访问,不支持迭代器.
## 定义
```cpp
#include <stack>
std::stack<TYPENAME, Container> s; // 使用Container作为底层容器
std::stack<TYPENAME> s; // 不指定Container时默认使用deque作为底层容器
```
## 常用函数
| 函数 | 作用 |
| --- | --- |
| `empty()` | 返回容器是否为空 |
| `size()`  | 返回容器中的元素数量 |
| `push(x)` | 将元素`x`插入栈中 |
| `pop()` | 删除栈顶元素 |
| `top()` | 访问栈顶元素(若为空则会出错) |

# 队列
STL队列`std::queue`是一种**先进先出**的容器适配器,仅支持查询或删除队首元素,不支持随机访问,不支持迭代器.
## 定义
```cpp
std::queue<TYPENAME, Container> q; // 使用Container作为底层容器
std::queue<TYPENAME> q; // 不指定Container时默认使用deque作为底层容器
```
## 常用函数
| 函数 | 作用 |
| --- | --- |
| `empty()` | 返回容器是否为空 |
| `size()`  | 返回容器中的元素数量 |
| `push(x)` | 将元素`x`插入队尾 |
| `pop()` | 删除队首元素 |
| `front()` | 访问队首元素(若为空则会出错) |

# 优先队列
优先队列`std::priority_queue`是一种堆,一般为二叉堆.
## 定义
```cpp
#include <queue>
std::priority_queue<TYPENAME> q; // 不指定Container时默认使用vector作为底层容器
std::priority_queue<TYPENAME, Container> q; // 指定Container作为底层容器
std::priority_queue<TYPENAME, Container, Compare> q;
// 指定Container作为底层容器,使用Compare作为比较类型
```
以下有几个注意事项:
1. 使用默认比较类型`less<TYPENAME>`时`top()`返回值反而为最大值.使用`greater<TYPENAME>`时返回最小值.
2. 不可跳过`Container`直接传入`Compare`.
3. 如果使用lambda函数自定义`Compare`,则需要将其作为构造函数的参数代入. `- ?`
```cpp
auto cmp = [](const std::pair<int, int> &l, const std::pair<int, int> &r) {
	return l.second < r.second;
};
std::priority_queue<std::pair<int, int>, std::vector<std::pair<int, int>>, decltype(cmp)> pq(cmp);
```
## 常用函数
| 函数 | 作用 |
| --- | --- |
| `top()` | 访问堆顶元素(不能为空) |
| `empty()` | 返回容器是否为空 |
| `size()` | 返回容器中的元素数量 |
| `push(x)` | 插入元素并对底层容器排序,复杂度$Ologn$ |
| `pop()` | 删除堆顶元素(不能为空),复杂度$Ologn$ |
## 小根堆示例
```cpp
struct cmp {
	bool operator ()(int a, int b) const {
		return a > b;
	}
};

priority_queue<int, vector<int>, cmp> q;
```
```cpp
bool compare(int a, int b) {
	return a > b;
}

auto cmp = [](int a, int b) {
	return a > b;
}

priority_queue<int, vector<int>, decltype(&compare)> pq(compare);
priority_queue<int, vector<int>, decltype(&cmp)> pq(cmp);
```
