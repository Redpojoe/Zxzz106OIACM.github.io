---
layout: default
title: "线段树模板"
date: 2018-07-16
category: [Template,Segment Tree]
tags: [模板,线段树]
---

# 线段树模板

## 概况

&emsp;线段树是一种很强大的数据结构，支持O(nlogn)地区间修改、查询极值、查询区间和，但常数比树状数组等同样是区间上的数据结构大。  
&emsp;一般来讲，处理区间问题考虑的数据结构顺序应为：  
&emsp;&emsp;前缀和->差分->树状数组->线段树->分块

## 代码

为适应不同题目需求，有不同的线段树打法 ~~其实就是改改结构体和Up~~  

#### 单点修改，区间查询

```cpp
struct node {
    int L, R, sum;
} tree[M << 2];
void up(int p) {
    tree[p].sum = tree[p << 1].sum + tree[p << 1 | 1].sum;
}
void Build(int L, int R, int p) {
    tree[p].L = L;
    tree[p].R = R;
    if (L == R) {
        tree[p].sum = A[L];
        return;
    }
    int mid = (L + R) >> 1;
    Build(L, mid, p << 1);
    Build(mid + 1, R, p << 1 | 1);
    up(p);
}
void Update(int x, int d, int p) {
    if (tree[p].L == tree[p].R) {
        tree[p].sum += d;
        return;
    }
    int mid = (tree[p].L + tree[p].R) >> 1;
    if (x <= mid)
        Update(x, d, p << 1);
    else
        Update(x, d, p << 1 | 1);
    up(p);
}
int Query(int L, int R, int p) {
    if (tree[p].L == L && tree[p].R == R)
        return tree[p].sum;
    int mid = tree[p].L + tree[p].R >> 1;
    if (R <= mid)return Query(L, R, p << 1);
    if (L > mid)return Query(L, R, p << 1 | 1);
    return Query(L, mid, p << 1) + Query(mid + 1, R, p << 1 | 1);
}
```

#### 区间修改，区间查询

```cpp
#include<stdio.h>
#include<string.h>
#define M 100005
#define LL long long
LL data[M], sum[M];
struct node {
    int L, R;
    LL add, sum;
} tree[M * 4];
void Build(int L, int R, int p) {
    tree[p].L = L, tree[p].R = R;
    tree[p].sum = tree[p].add = 0;
    if (L == R)return;
    int mid = (L + R) >> 1;
    Build(L, mid, 2 * p);
    Build(mid + 1, R, 2 * p + 1);
}
void Up(int p) {
    tree[p].sum = tree[2 * p].sum + tree[2 * p + 1].sum;
}
void Down(int p) {
    if (tree[p].add == 0)return;
    tree[2 * p].sum += tree[p].add * (tree[2 * p].R - tree[2 * p].L + 1);
    tree[2 * p].add += tree[p].add;
    tree[2 * p + 1].sum += tree[p].add * (tree[2 * p + 1].R - tree[2 * p + 1].L + 1);
    tree[2 * p + 1].add += tree[p].add;
    tree[p].add = 0;
}
void Update(int L, int R, LL add, int p) {
    if (tree[p].L == L && tree[p].R == R) {
        tree[p].sum += (R - L + 1) * add;
        tree[p].add += add;
        return;
    }
    Down(p);
    int mid = (tree[p].L + tree[p].R) >> 1;
    if (mid >= R)Update(L, R, add, 2 * p);
    else if (mid < L)Update(L, R, add, 2 * p + 1);
    else {
        Update(L, mid, add, 2 * p);
        Update(mid + 1, R, add, 2 * p + 1);
    }
    Up(p);
}
LL Query(int L, int R, int p) {
    if (tree[p].L == L && tree[p].R == R) {
        return tree[p].sum;
    }
    Down(p);
    int mid = (tree[p].L + tree[p].R) >> 1;
    if (R <= mid)return Query(L, R, 2 * p);
    else if (L > mid)return Query(L, R, 2 * p + 1);
    else  return Query(L, mid, 2 * p) + Query(mid + 1, R, 2 * p + 1);
}
```