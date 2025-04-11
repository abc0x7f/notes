*Writen by 周子未*
```table-of-contents
title: 
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 0 # Include headings up to the specified level
includeLinks: true # Make headings clickable
hideWhenEmpty: false # Hide TOC if no headings are found
debugInConsole: false # Print debug info in Obsidian console
```
# 代码规范
1. 初学时可以使用`#include <bits/stdc++.h>`(万能头文件)
2. 左括号可换行可不换行(如`{`,老师要求换行)
3. 不能有两个连续空行,独立的代码块之间要有空行;头文件块`#include`,函数,全局变量块等必须用空行隔开.
4. 空格的作用:识别族群的位置.
>前后必须都有空格: 冒号`:`,双目运算符`+, -, &, |, >>, ...`,三目运算符`?`.
>前加后不加: 地址与指针运算符(目前未学).
>后加前不加: 关键字`if,return,while,for, ...`(会特殊高亮),逗号,分号等.
>前后都不加`.`,`->`,`::`,以及单目运算符`!`,`-`,`++`,`--`.

5. 注意**缩进**,同一逻辑层下的代码缩进要相同.
## 代码示例
```cpp
#include <bits/stdc++.h>
using namespace std;

int main()
{
	int x, cnt = 0, notPri[505], pri[505];
	memset(notPri, 0, sizeof notPri);
	notPri[0] = notPri[1] = 1;
	
	cin >> x;
	
	for (int i = 2; i < 505; i++)
	{
		if (!notPri[i]) pri[++cnt] = i;
		for (int j = 1; j <= cnt && i * pri[j] < 505; j++)
		{
			notPri[i * pri[j]] = 1;
			if (i % pri[j] == 0) break;
		}
	}
	
	cout << (notPri[x] ? "合数" : "质数") << endl;
}
```

# 分支
`if-else`语句符合**就近原则**,每一块都以`if`开头,注意每个`else if`/`else`是属于哪个`if`.
同组的`if`,`else if`,`else`永远只会执行一个.
其他的点只有跟着代码想一遍逻辑,不要遗漏和重复即可.
```cpp
int x = 5;
if (x <= 10) cout << 1 << " ";
if (x <= 100) cout << 2 << " ";
if (x <= 5) cout << 3 << " ";
else if (x <= 50) cout << 4 << " ";
if (x <= 1) cout << 5 << " ";
else if (x <= 3) cout << 6 << " ";
else cout << 7 << " ";
```
> 输出
1 2 3 7
### 例: 输入一个坐标(x,y)求该点在第几象限或在哪个半轴
```cpp
int x, y;
cin >> x >> y;
if (x > 0) // 1.1
	if (y > 0) cout << "第一象限" << endl; // 2.1
	else if (!y) cout << "x正半轴" << endl; // 2.2
	else cout << "第四象限" << endl; // 2.3
else if (x < 0) // 1.2
	if (y > 0) cout << "第二象限" << endl; // 3.1
	else if (!y) cout << "x负半轴" << endl; // 3.2
	else cout << "第三象限" << endl; //3.3
else // 1.3
	if (y > 0) cout << "y正半轴" << endl; //4.1
	if (!y) cout << "原点" << endl; // 4.2
	else cout << "y负半轴" << endl; // 4.3
return 0;
```
# 循环
## while循环
![while循环流程图](./C1/1.png)
```cpp
while (布尔表达式) {
	// 语句块
}
// 后续语句
```
## 死循环
上述代码中如果布尔表达式一直为真,循环永远不会自己结束,即形成了死循环.
如``while(1){}``就是一种死循环的写法.
但是我们可以通过`break`和`continue`控制循环的进行.
`break`用于**终止**当前层循环,并执行后续语句.
`continue`用于跳过本次循环的后续语句,并立即开始下一次循环迭代.它**不会结束**当前循环.
```cpp
while (1) {
	AAA;
	if (XXX) break;
	if (YYY) continue;
	BBB;
	if (ZZZ) break;
}
CCC;
```
上述代码中:
1. 每次循环先执行`AAA`语句.
2. 如果某次循环满足`XXX`则直接结束循环,接着执行循环外的`CCC`.
3. 如果某次循环不满足`XXX`而满足`YYY`,则不执行本次循环中的`BBB`直接开始下一次循环.
4. 执行`BBB`语句.
5. 如果某次循环`XXX`和`YYY`都不满足而满足`ZZZ`,则在执行完`AAA`和`BBB`后结束循环并执行`CCC`.
## do...while循环
![do...while循环流程图](./C1/2.png)
```cpp
do {
// 语句块
} while (布尔表达式);
```
`do...while`循环无论布尔表达式是否为真,都会**执行一次**语句块.
## for循环
![for循环流程图](./C1/3.png)
```cpp
for(初始化; 布尔表达式; 迭代){
	// 语句块
}
```
上述代码中:
1. 无论布尔表达式是否为真,都会**执行一次**初始化.
2. 循环结束的条件为`布尔表达式为假`.
3. 每次循环除了会执行一次语句块,还会再执行一次迭代.
4. 如果省略布尔表达式,即`for(初始化; ; 迭代){}`,则默认表达式为真,循环永远不会结束.
所以for循环也可以这样写:
```cpp
初始
for(; ;) {

}
```
## 从1到n的循环
```cpp
for (int i = 1; i <= n; i++) {
	// 总共进行i次循环
	// i的值从1到n
}
```
等价于:
```cpp
int k = 1;
while (k <= n) {
	// 此处可进行有关k的计算
	k++;
}
```
注意`for`的圆括号里定义的变量是**临时变量**,只能在花括号内使用.
```cpp
for (int i = 1; i <= n; i++) {
	// i只能在花括号里使用	
}
cout << i << endl; //这样会报错
```
报错为:
```
'i' was not declared in this scope
// i未在此范围内声明
```
### 例: 计算$\displaystyle\sum_{k=1}^nk^2$
```cpp
int sum = 0;
for (int i = 1; i <= n; i++) {
	sum += i * i;
}
cout << sum << endl;
```

## 取x的各个位上的数
```cpp
for (; x; x /= 10) {
	cout << x % 10 << endl; // x % 10 就是x当前位的数字
}
```
等价于
```cpp
while (x) {
	cout << x % 10 << endl;
	x /= 10;
}
```
### 例: 输入数x,将x各个位倒序输出
>输入
>12334
>输出
>4 3 3 2 1
```cpp
int a[25], k = 0, x;
cin >> x;
for (; x; x /= 10) {
	a[++k] = x % 10;
}
for (int i = 1; i <= k; i++) 
 cout << a[i] << " ";
```
# 数组常用套路
## 一维数组的定义
数组用于存储**多个相同类型**的元素,它本质上是连续内存空间的集合;
```cpp
int N = 10;
int a[100];
int b[5] = {2, 1, 3, 5, 4};
// b[0] = 2,b[1] = 1,依此类推
char c[N];
```
以下有几个注意事项:
1. 数组序号从0开始,`int a[10];`定义的数组能使用的范围为`a[0]~a[9]`.
2. 由于数组的本质是连续内存空间的集合,所以就算写出`a[-1]`,`a[10]`也不一定会报错,但是结果肯定是错的.
3. 在`main()`函数里定义的数组(及变量)如果不赋初始值会被随机赋值.
```cpp
int x, a[10];
cout << x << " " << a[10] << endl;
// 以上两个都会输出随机值
```
### 例: 输入n(n<=20),再输入n个正整数,求其中的最小值和它是第几个数,有多个最小值时优先输出序号大的
```cpp
int n, a[25], im = 100000, k;
// 因为im要不断跟数组里的最小值比较,所以初值必须非常大;
cin >> n;
for (int i = 1; i <= n; i++) cin >> a[i];
for (int i = 1; i <= n; i++)
	if (im >= a[i]) im = a[i], k = i;
cout << a[i] << " " << k << endl;
```
如果优先输出序号小的,只需将上述第6行进行如下修改`想想为什么`
```cpp
	if (im > a[i]) im = a[i], k = i;
```
## 二维数组的定义
二维数组`a[n][m]`可想象成一个$n$行$m$列的矩阵,但行列的**初始编号为0**.
比如`int a[2][3];`所对的6个元素`a[i][j]`:

| |$j=0$|$j=1$|$j=2$|
| --- | --- | --- | --- |
| $i=0$| $a[0][0]$| |
| $i=1$| | | $a[1][2]$|
### 例: 输入n,m(n,m<=10)并给定一个n\*m的矩阵,输出其转置
```cpp
int n, m, a[15][15], b[15][15];
cin >> n >> m;
for (int i = 1; i <= n; i++)
	for (int j = 1; j <= m; j++)
		cin >> a[i][j];
for (int i = 1; i <= m; i++)
	for (int j = 1; j <= i; j++)
		b[i][j] = a[j][i];
for (int i = 1; i <= m; i++) {
	for (int j = 1; j <= n; j++)
		cout << b[i][j] << " ";
	cout << endl;
}
```
### 例: 给定一个5\*5的矩阵,将其强行转化为上三角矩阵
>输入
>1 2 3 4 5
>5 4 3 2 1
>1 1 1 1 1
>2 2 2 2 2
>3 3 3 3 3

>输出
>1 2 3 4 5
>0 4 3 2 1
>0 0 1 1 1
>0 0 0 2 2
>0 0 0 0 3
```cpp
int a[5][5];
for (int i = 0; i < 5; i++)
	for (int j = 0; j < 5; j++)
		cin >> a[i][j];
for (int i = 0; i < 5; i++)
	for (int j = 0; j < 5; j++)
		if (i + (4 - j) >= 5) a[i][j] = 0;
for (int i = 0; i < 5; i++) {
	for (int j = 0; j < 5; j++)
		cout << a[i][j] << " ";
	cout << endl;
}
```
# 字符串常用套路
## ASCII码
char类型保存的是字符的ascii码值.
```cpp
char c = '0', s = 67;
cout << (int)c << " " << s << endl;
```
>输出
>48 C
## 用字符数组做字符串处理
```cpp
char c, s[25];
c = getchar(); // 输入一个字符
for (int i = 0; i < 10; i++) s[i] = getchar();
putchar(c);
for (int i = 0; i < 5; i++) putchar(s[i]);
cin.getline(s, 20, ' '); // 为s读取19个字符直至读取到空格
// 等等
```
此处不展开,可以直接看学习通.
## C++封装的字符串处理
c++封装了`string`类用于处理字符串.`string`的用法类似`int`.
`string s1;`所定义的变量本身就是一个字符串,而不是`char`所定义的单个字符.
所以,如果`string s1;`的`s1`不为空,那么就可以用`s1[i]`这样的方式输出`s1`的第$i$个字符.(编号从0开始)
```cpp
string s1, s2, s3; // 类似int的定义方式
cin >> s1 >> s2 >> s3;
cout << s1 << " " << s2 << " " << s3 << endl;
```
只有在读到换行`\n`和空格` `等字符时,才会结束当前`string`变量的输入.
>输入
>12$%,8 !:\n()p
>abc0x7f

>输出
>12$%,8 !:\n()p abc0x7f
### string的常用函数
再次注意`string`的编号是从0开始的.
```cpp
string s, s1;
cin >> s >> s1;
cout << s.size() << endl; // 字符串s的长度,以前也写作s.length()
for (int i = 0; i < s.size(); i++) cout << s[i] << " "; // 按数组方式输出字符
cout << endl;
cout << s.substr(1, 3) << endl; // 输出s位置1~3上的子串
if (s.find(s1) != string::npos) cout << s.find(s1) << endl;
else cout << -1 << endl;
// 寻找s1在s中出现的位置,如果没有出现则返回特殊值string::npos
s += s1; cout << s << endl; // string重载了+号,a + b表示将b拼接在a后面
cout << (s == s1) << " " << (s1 == "34") << endl;
// string重载了==号,若两个字符串完全相等则返回真,否则返回假
// 等等更多内置函数
```
>输入
>12345 34

>输出
>5
>1 2 3 4 5
>234
>2
>1234534
>0 1

一般情况下**尽可能使用**`string`类型(不会被换行`\n`和空格` `字符干扰).
如果在做C++实验的时候题目要求定义字符数组`char a[n];`,那么按要求定义但不使用即可.
### 例: 输入一个字符串,如果是形如`https://A.com/`格式(A只能是英文字母和数字组成的字符串,长度6~10),则输出"YES",否则输出"ERR"
```cpp
char a[23]; // 定义但不使用
string s, s1 = "https://", s2 = ".com";
cin >> s;
if (s.size() < 18 || s.size() > 22) {
	cout << "ERR" << endl;
	return 0;
}
for (int i = 0; i < 8; i++)
	if (s[i] != s1[i]) {
		cout << "ERR" << endl;
		return 0;
	} // 确认前缀
for (int i = 0; i < s2.size(); i++)
	if (s[s.size() - 1 - i] != s2[s2.size() - 1 - i]) {
		cout << "ERR" << endl;
		return 0;
	} // 确认后缀
for (int i = 8; i < s.size() - 5; i++)
	if ((s[i] < 65 || s[i] > 90) && (s[i] < 97 || s[i] > 122) && (s[i] < 48 || s[i] > 57)) {
		cout << "ERR" << endl;
		return 0;
	} // 确认A是否只由数字字母组成
cout << "YES" << endl;
```
当然上例的各个部分可以用内置函数简化,此处不展开.
# 解决问题的思想
## 问题的拆解
### 例: 输入数n,求[1,n]上质数的个数
有时候问题并不是一步就能解决的,需要把问题**拆解成更小的问题**逐个解决.
对于上面这个问题,我们先来看给定一个数$x$,怎么判断是不是质数.
假设$x$不是质数,那么一定可以被分解成$x=a\times b\ (a,b\in N_+且a,b\geq2)$.
同时$a,b$中至少有一个小于等于$\sqrt{x}$.`为什么?`
所以判断$x$是不是质数时,只需要从$2$枚举到$\sqrt{x}$,如果$x$被其中任意一个数整除,那么$x$不是质数,反之$x$是质数.
```cpp
int x;
cin >> x;
bool pri = 1;
for (int i = 2; i * i <= x; i++)
	if (x % i == 0) {
		pri = 0;
		break;
	}
if (pri == 0) cout << "NO" << endl;
else cout << "YES" << endl;
```
回过头来看问题,我们只需要对[2,n]上的每一个数执行上述的过程即可
```cpp
int n, s = 0;
cin >> n;
for (int i = 2; i <= n; i ++) {
	int pri = 1; // 注意定义变量的位置,花括号里定义的变量只能在花括号里的本次循环中使用;
	// 即每次i的值改变(即循环进行一次),上一次的变量pri都会自动注销,并新定义一个pri = 0.
	for (int j = 2; j * j <= i; j ++)
		if (i % j == 0) {
			pri = 0;
			break;
		}
	if (pri == 1) s++;
	//if(pri == 0) cout << i << " ";
	// 假如需要输出有哪些质数,将上面一行取消注释.
}
cout << s << endl;
```
### 例: 输入10个数,将它们从大到小输出
>题目意思就是将输入的数字排序,排序有很多种思路,这里介绍一种.

从大到小输出用另一种说法就是,先输出最大的,再输出第二大的,...
如果我们找到了最大的数,并将其拿走,那么原第二大数的就变成新的最大的数,问题又转化为寻找最大的数.
所以还是先看怎么找出最大的数和它的位置:
```cpp
int k, iM = -100000; // 题目中没说输入为正整数
for (int i = 0; i < 10; i++)
	if (im < a[i]) iM = a[i], k = i;
```
那么我们如何实现将第$i$大的数拿走的操作呢?
只需要每次将第$i$大的数与第$i$个数`a[i]`交换,接着再寻找`a[i+1]`到`a[n]`中最大的数$p$,此时$p$必定为第$i+1$大的数.
我们再将$p$与`a[i+1]`交换,不断重复这个操作即可.
```cpp
int a[15];
for (int i = 0; i < 10; i++) cin >> a[i];
for (int i = 0; i < 10; i ++) {
	int k = i, iM = -100000; // k赋初值防止越界(本写法可不赋值,但编译器会警告)
	for (int j = i; j < 10; j++)
		if (iM < a[j]) iM = a[j], k = j;
	// 交换a[i]和a[k](a[k]为最大值)
	int t = a[i];
	a[i] = a[k];
	a[k] = t;
}
for (int i = 0; i < 10; i++) cout << a[i] << " ";
cout << endl;
```