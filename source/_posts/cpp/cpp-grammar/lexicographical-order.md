---
title: 字符串数组以字典序排序
date: 2019-8-20
tags:
- 数据结构
- C++
category:
- C++
- C++语法
---

```c++
bool operator < (char * a,char * b)
{
    int l = min(strlen(a), strlen(b));
    for (int i = 0; i < l; i++)
    {
        if (a[i] < b[i]) return 1;
        if (a[i] > b[i]) return 0;
    }
    return strlen(a) < strlen(b);
}
```

注意，就数字集合 {1, 2, 3, ..., n} 的排列而言，这个集合的全排列本身可以看成是 n 进制的数，这种情况下，所有排列的字典序等价于所有按照全排列顺序把数字写成的数集合的升序。**而不是把数转成字符串再按字典序排序**！！！！！！

顺便，1~11 的字典序排序为 `1 10 11 2 3 4 5 6 7 8 9`.