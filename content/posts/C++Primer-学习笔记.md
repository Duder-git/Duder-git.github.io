---
title: "C++Primer"
date: 2023-04-03T22:12:49+08:00
draft: false
tags: [C++]
categories: [技术分享]
featured_image: 
description: 
---

# C++ Primer 学习笔记

西安 大唐芙蓉园 望春阁

![](/images/C++Primer-学习笔记/IMG_0061.JPG)

## 写在前面

本文学习教材是《C++Priner中文版》第五版，主要用于记录C++学习过程中的要点，对于初学者（本人）起到提示和快速复习的作用。

本文以时间为轴，记录系统学习C++的过程，意在不虚度光阴，不沉浸虚无。

在科研之余抽身出来，从更广大的视角俯视当前所学，避免思维精力锁死单一方向。

## 2023.03.30

### 变量

#### 字符变量

> 一个字 四字节 
>
> 一个字节 8比特
>
> 一个字 32比特或者64比特



> - (a) 'a', L'a', "a", L"a"
>
>   字符字面量、宽字符字面量、字符串字面量、字符串宽字符字面量
>
> - (b) 10、10u、10L、10uL、012、0xC
>
>   十进制、无符号十进制、长十进制、无符号长十进制、八进制、十六进制
>
> - (c) 3.14、3.14f、3.14L
>
>   double、float、long double
>
> - (d) 10, 10u, 10., 10e-2
>
>   十进制、无符号十进制、double、double



定义变量时没有指定初值，变量被默认初始化

> 内置类型变量 未被显式初始化 
>
> ​	函数体之外的初始化为0
>
> ​	函数体内部内置类型变量不被初始化

！ 建议初始化每一个内置类型变量



#### 声明和定义

声明：使名字为程序所知

定义：创建与名字关联的实体

> 如果要声明而非定义，在变量前添加关键字extern
>
> 试图初始化extern关键字标记的变量，将引发错误



#### 变量名规范

> * 体现实际含义
> * 一般小写
> * 自定义类名大学字母开头
> * 多个单词组成使用“_”连接



## 2023.03.31

###引用和指针

#### 引用

在初始化变量时，初始值会被拷贝到新建对象中。在定义引用时，程序把引用和初始值绑定在一起，而不是将初始值拷贝给引用。

> 引用并非对象，相反，他只是为一个已经存在的对象七点另一个名字

```c++
int i, &ri = i;
i = 5; ri = 10
std::cout<<i<<" "<<ri<<std::endl;
```

> 10 10

#### 指针

指针本身是一个对象，允许对指针赋值和拷贝，而且在指针的声明周期内可以先后指向几个不同的对象。

无需在定义时赋初值。

```c++
int ival = 42;
int *p = &ival;
cout<<*p;    	// 由符号*得到指针p所指对象，，输出42
double dval;
double *pd = &dval;
int *pi = pd; 	//错误，指针类型不匹配
pi = &dval;		// 错误，试图把double地址赋给int
```

> 指针存放在某个对象地址，获取地址使用取地址符&。
>
> 指针类型要与指向对象严格匹配

#### 符号多重含义

```c++
int i = 42;
int &r = i; 	// 引用，&是声明的一部分
int *p;     	// 指针，*是声明的一部分
p = &i;     	// 取地址符
*p = i;     	// 解引用
int &r2 = *p; 	// &引用，*解引用
```

#### 赋值和指针

指针和引用都能提供对其他对象的间接访问，但引用本身并非为一个对象，指针可以存放一个新的地址，从而指向一个新的对象

```c++
int i = 42;
int *pi = 0; 	// pi被初始化，但没有指向任何对象
int *pi2 = &i;	// pi2被初始化，存有i的地址
int *pi3; 		// pi3定义于块内，则pi3的值无法确定

pi3 = pi2; 		// pi3和pi2指向同一个对象i

pi = &ival; 	// pi值改变，指向ival
*pi = 0;   		// ival值被改变，指针pi并没有改变
```

> 一条赋值语句到底改变了指针的值还是改变了指针所指对象的值，赋值永远改变的是等号左侧的对象



```c++
int *p
if(p)  	// 判断p是否为nullptr
if(*p)  // 判断p指向的值是否为0
```

> 任何非0指针对应的条件值都是true



#### void* 指针

```c++
double obj = 3.14,
double *pd = &obj;
void *pv = &obj;   // 成立，obj可以是任意类型的对象
pv = pd; 		   // pv可以存放任意类型指针
```



#### 指针和引用的主要区别

> 1. 引用是已存在对象的另一个名字,指针本身就是一个对象
> 2. 初始化,引用仍然绑定到他的初始对象,无法重新绑定,指针可以分配和复制
> 3. 引用始终获取引用最初绑定的对象,单个指针在其生命周期内可以指向多个不同对象
> 4. 必须初始化引用,指针在定义时无需初始化



#### 指向指针的指针

```c++
int ival =1024;
int *p = &ival;
int **p2 = &p;
cout<< ival<<endl;
cout<< *p <<endl; // 解引用
cout<< **P2 <<endl;  // 解两层引用
```

#### 指向指针的引用

```c++
int i= 42;
int *p;			// p是一个int指针
int *&r = p;    // r是一个对指针p的引用
r = &i;			// 给r幅值&i,令p指向i
*r = 0;     	// 解引用r得到i,p指向i,i值改为0
```



###  const

> 常量引用是对const引用

```c++
int i = 42;
const int &r1 = i;		// 合法
const int &r2 = r1;		// 合法
const int &r3 = r1*2;   // 合法
int &r4 = r1 * 2;		// 错误，r4是一个普通非常量引用
```

#### 指针和const

与引用一样，可以令指针指向常量或非常量。

指向常量的指针不能用于改变其所指对象的值。

```c++
const double pi = 3.14;
const double *cptr = &pi;
*cptr = 42; // 错误，不能给*cptr赋值
```



```c++
int i = -1, &r = 0;         // 不合法, r必须引用对象.
int *const p2 = &i2;        // 合法.
const int i = -1, &r = 0;   // 合法.
const int *const p3 = &i2;  // 合法.
const int *p1 = &i2;        // 合法.
const int &const r2;       // 不合法, r2引用不可以是常量
const int i2 = i, &r = i;   // 合法.
```



#### 顶层const

**顶层const**指针本身是常量，不能改变本身的值；

**底层const**指针所指对象是一个常量，可以改变指针指向；



#### 常量表达式

> 值不会变并且在编译过程中就能得到计算结果的表达式。

```c++
const int amx_files = 20;  // 常量表达式
const int sz = get_size(); // 不是常量表达式，在运行后才知道具体数值
```



#### constexpr常量

> C++11规定，允许将变量声明为constexpr类型，一边用编译器验证
>
> 你认定一个变量时常量表达式，就把他声明为constexpr类型

```c++
// P是一个指向整型常数的指针
const int *p = nullptr;
// q是一个指向整数的常量指针
constexpr int *q = nullptr;
```

## 2023.04.02

### 类型

#### 类型别名

typedef

```c++
typedef double wages; // wages是double的同义词
typeeef wages base, *p;  // base是double的同义词，p是double*的同义词
```

别名声明

```c++
using SI = Sales_item; // SI是Sale_item的同义词
```

#### auto

> auto可以在一条语句中声明多个变量，但是一个声明语句只能有一个基本数据类型，所以该语句中所有变量的初始基本数据类型必须一样。

```c++
auto i = 0, *p = &i; // 正确
auto sz = 0, pi = 3.14; // 错误
```

#### decltype

> 从表达式类型推断定义变量的类型，但不想用该表达式的值初始化变量
>
> decltype(()) 结果永远是引用，decltype()只有当本身是一个引用时才是引用
>
> 赋值产生引用效果

```c++
decltype(f()) sum = x; // sum的类型就是函数f的返回类型
decltype((i)) d;    	// 错误，d是int&，必须初始化
decltype(i) e;			// 正确，e是一个未初始化的int
decltype(i = a) b=c;   	// b是引用 
```

### 自定义数据结构

```c++
# ifndef SALES_DATA_H
# define SALES_DATA_H
#include <string>
struct Sales_data {

};
# endef
```

## 2023.04.03

#### string

```c++
string S1;		   	// 默认初始化
string S2(S1);		// s2是s1的副本
string S2 = S1;		// s2是s1的副本
string S3("value");	// S3是value副本
string S3 = "value";// S3是value副本
string S4(n,'c')	// 把s4初始化为连续n个字符c组成的串
```

直接初始化和拷贝初始化

```c++
string s5 = "hiya";		// 拷贝初始化
string s6("hiya");		// 直接初始化
string S7(5,'c');		// ccccc
```

读取未知数量string

```c++
int main()
{
	string word;
	while (cin>>word)
		cout << word << endl;
	return 0;
}

int main()
{
    string line;
    while(getline(cin,line))
        cout<<line<<endl;
    return 0;
}
```

empty()

size()

```c++
string s1 = "hello";
string s2 = s1 + ",";
string s3 = "Hello" + "World";  // 错误
string s4 = "Hello" + "，" + s1； // 错误
```



```c++
string s("Hello World!!!");
for (auto &c : s)
    c = toupper(c); // c是引用，改变s值
cout << s << endl;
```

while for auto &c

```c++
int main()
{
    string str("a simple string");
    
    // while
    decltype(str.size()) i = 0;
    while (i < str.size()) str[i++] = 'X';
    cout << str << endl;

    // for
    decltype(str.size()) i = 0;
    for (i = 0; i < str.size(); str[i++] = 'Y');
    cout << str << endl;
	
    // string
    for (auto &c : str) c = 'X';
    cout << str << endl;
    
    return 0;
}
```
