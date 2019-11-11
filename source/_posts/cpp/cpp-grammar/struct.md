---
title: C++ 结构体
date: 2019-8-19
tags:
category:
- C++
- C++语法
---

C++ 中的结构体结合了类，于是就有很多很有意思的写法。

## 构造函数

```c++
struct teamS {
       int s; //solved
       int p; //penalty
       teamS() {};
       teamS(int _s = 1, int _p = 2):s(_s), p(_p){}
};

teamS s(6,66);
```

## 重载 `[]` 使结构变为类似于数组的形式

起初是看到 map 在这么用，试了一下，发现没有报错，有点香。

对一维数组重载，记得使用引用 `&`。

```c++
struct triple
{
    int first;
    int second;
    int third;
    int & operator [](int i)
    {
        switch (i)
        {
        case 0: return first;
        case 1:return second;
        case 2:return third;
        }
    }
}
```

对二维数组的重载，使用的是指针 `*`，就不需要引用了。

```c++
struct matrix
{
    long long v[3][3] = { 0 };
    long long * operator[](int i)
    {
        return v[i];
    }
}m;

m[1][2] == m.v[1][2];
```

## 运算符重载

C++引入了运算符重载，并有以下规则：

1. 只能重载已有的运算符，已有的少部分也不能重载（`::`、`#` 等）；
2. 重载以后的优先级不变。

运算符重载的格式为：

```c++
class Complex
{
    double real, imagine;
    public: /*...*/
        Complex() {};
    	Complex(int r = 0, int i = 0) {};
        Complex operator + (Complex num) { /* */ }
}c1,c2;
c1 = c2 + 1;
c1 = c2.operator+(1);
```

但是无法使用 `c1 = 1 + c2`，因为重载的 `+` 是属于 `Complex` 类的，而不是 `int`。  

正确的使用方法是：把该重载声明为 `Complex` 类以外的函数（如果函数需要访问 `Complex` 的 `private` 成员，注意使用友元关键字）

```c++
friend Complex operator + (Complex num, Complex C) {/* */}
```

这样，编译器就能愉快的把 `int` 转换为 `Complex` 了。

下面写几个值得一提的特殊的运算符重载。

## 类型转换函数

把 `int` 当作一个一元操作符可还行。

```c++
struct teamS {
    int s; //solved
    int p; //penalty
    operator int()
    {
        return s * 100 - p;
    }
};
```

### 重载 `++` 自增运算符

> 转自：https://blog.csdn.net/anye3000/article/details/6618495

我写类的时候，重载了 `++` 运算符，然后 `date++` VS 报错。查了以后，才意识到，`++` 分了前置/前缀形式和后置重载/后缀形式。

```c++
class A
{
private:
    int m_i;
public:

    //++i
    A& operator++()
	{
		++m_i;
		return *this;
	}
	//i++
	const A operator++(int)
	{
		A tmp = *this;
		++(*this);
		return A(tmp);
	}
}
```

注意：

1. 为了区分前后，用 `++()` 表示前自增，用 `++(int)`后自增。
2. **前自增应该返回引用 `A&`**，因为按照前自增的标准定义，应该支持 `++++a` 的语法，而且两次前自增都应该是对 a 对象的自身操作。如果返回A类型，那第二次前自增调用的是临时对象的前自增操作，和定义也不同；
3. **后自增应该返回 `const`**，这可以防止形如 `a++++` 的用法。不能返回 `const &`，因为实现里面返回的是临时的 `temp`，不能返回临时的指针。所以就涉及到了复制构造（Copy Construction）的问题了额。还是**多用前自增吧……**
4. 一般通过前自增操作来实现后自增操作符函数。

### 重载等于 `=`

重载 `=` 和拷贝构造函数很相似，于是放在[拷贝构造函数](../class-and-object/#拷贝构造函数)一节。