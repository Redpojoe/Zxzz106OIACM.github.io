---
layout: default
title: "离散化模板"
date: 2018-01-01
category: Template
tags: [模板,离散化]
---

# 离散化模板

## 定义
>&emsp;离散化，把无限空间中有限的个体映射到有限的空间中去，以此提高算法的时空效率。  
>&emsp;通俗的说，离散化是在不改变数据相对大小的条件下，对数据进行相应的缩小。

## 流程
1. 1.排序
2. 2.删除重复元素
3. 3.索引元素离散化后对应的值

## 代码

一种是通过STL实现的，适用于有重序列  

```C++
int a[M], t[M];
int n;
scanf("%d",&n);
for(int i=1; i<=n; i++)
    scanf("%d",a[i]),t[i]=a[i];
sort(t+1,t+n+1);
m=unique(t+1,t+1+n)-t-1;//m为不重复的元素的个数，若需保留则不需要这句话
for(int i=1; i<=n; i++)
    a[i]=lower_bound(t+1,t+1+m,a[i])-t;
```

另一种区别不大，适用于无重序列，效率较低

```C++
struct node {
    int x, idx;
    bool operator < (const node &rhs) const {
        return x < rhs.x;
    }
};
node dcr[M];
int A[M];
int n;
scanf("%d",&n);
for(int i = 1; i <= n; i++) {
    scanf("%d", &dcr[i].x);
    dcr[i].idx = i;
}
sort(dcr+1,dcr+n+1);
for(int i = 1; i <= n; i++) {
    A[dcr[i].idx] = i;
}
```