---
title: 数模自学笔记
date: 2020-04-18 10:27:07
tags:
- 数学建模
category:
- 数学建模
mathjax: true
top: 1
---

## 第一二周 线性规划 整数规划

时间：2020.4.13-2020.4.26

### 国赛 2009D 会议筹备

知识点：线性规划、整数规划、多目标规划、线性回归。

> 题目链接：http://special.univs.cn/service/jianmo/sxjmtmhb/2009/1009/864452.shtml
> 优秀论文：https://wenku.baidu.com/view/d32ba04669eae009581bec2c.html
> PPT 讲解：https://wenku.baidu.com/view/67e207a6284ac850ad024229.html?rec_flag=default&sxts=1587173703951
> 上面两个资料各有优缺点，可以对比参考。
> 优秀论文 2：https://wenku.baidu.com/view/5e238f01de80d4d8d15a4f73.html
> 简化版的题目的建模，简化为整数建模：https://wenku.baidu.com/view/5c1657c03186bceb19e8bbef.html

> 请你们通过数学建模方法，从经济、方便、代表满意等方面，为会议筹备组制定一个预订宾馆客房、租借会议室、租用客车的合理方案。

审题：从三个方面分析，应该看出来这是多目标规划。

> 宾馆的预定与会议室的租借都是 0—1 规划模型，我们在考虑宾馆和会议室的时候，当宾馆预订时，此会议室可以开，也可以不开，但是当某个会议室租借时，对应的宾馆就必须预订。
 
宾馆和会议室之间的对应关系为 $y_{ij}\leq x_{ij}$。

> 租车要考虑多少代表参加哪个分组会议，题目中没有这方面的信息，可以按照**平均的、随机的**方式处理。

题目没有提到的东西，就可以假设为**平均的、随机的**。用好这些假设，简化问题。

> 优化的约束条件中有：
> 
> $$y=\begin{cases}
1 & x > 0 \\\\
0 & x = 0
\end{cases}$$

显然该约束条件无法在 MATLAB 中直接调用 `intlinprog` 求解。

可以将约束条件转化为：

$$\varepsilon x \leq y \leq Mx$$

其中 $\varepsilon$ 为足够小的数，$M$ 为足够大的数。

更多的非线性规划问题转化为线性规划问题的方式可看[优化 | 线性规划和整数规划的若干建模技巧](https://zhuanlan.zhihu.com/p/69397833)。
