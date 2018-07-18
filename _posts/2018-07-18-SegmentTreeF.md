---
layout: default
title: "离散化"
date: 2018-07-18
category: Segment Tree
tags: [线段树,离散化]
---

# 线段树专题

## 离散化

[题目链接](https://cn.vjudge.net/problem/HihoCoder-1079)  

## 思路
既然题目叫“离散化”，自然要用离散化来解  

离散化也大概是套路了：

1. 1.读入
2. 2.排序
3. 3.离散

```C++
for(int i=1; i<=n; i++){
    Rd(A[++top].x);
    A[top].n=i;
    Rd(A[++top].x);
    A[top].n=i+n;
}//读入
sort(A+1,A+1+top);//排序
for(int i=1; i<=top; i++) {
    if(A[i].n>n)b[A[i].n-n]=cnt;
    else a[A[i].n]=cnt;
    if(A[i].x!=A[i+1].x)cnt++;
}//带去重的离散化
```

其余部分用线段树基本就是模板

## 代码

```C++
#include<bits/stdc++.h>
using namespace std;
const int M=100015;
namespace IO {
    const int MT = 10 * 1024 * 1024;
    char IO_BUF[MT];
    int IO_PTR, IO_SZ;
    void begin() {
        IO_PTR = 0;
        IO_SZ = fread (IO_BUF, 1, MT, stdin);
    }
    template<typename T>
    inline void Rd (T & t) {
        while (IO_PTR < IO_SZ && IO_BUF[IO_PTR] != '-' && (IO_BUF[IO_PTR] < '0' || IO_BUF[IO_PTR] > '9'))
            IO_PTR ++;
        bool sgn = false;
        if (IO_BUF[IO_PTR] == '-') sgn = true, IO_PTR ++;
        for (t = 0; IO_PTR < IO_SZ && '0' <= IO_BUF[IO_PTR] && IO_BUF[IO_PTR] <= '9'; IO_PTR ++)
            t = t * 10 + IO_BUF[IO_PTR] - '0';
        if (sgn) t = -t;
    }
    template<typename T>
    inline void print(T x) {
        static char s[33], *s1; s1 = s;
        if (!x) *s1++ = '0';
        if (x < 0) putchar('-'), x = -x;
        while(x) *s1++ = (x % 10 + '0'), x /= 10;
        while(s1-- != s) putchar(*s1);
    }
    template<typename T>
    inline void println(T x) {
        print(x); putchar(' ');
    }
};
using namespace IO;
int n,top,x,y,cnt=1,l,k;
int a[M],b[M],vis[M];
struct node{
    int x,n;
    bool operator <(const node &_)const{
            return x<_.x;
    }
} A[M<<1];
int tree[M<<4];
void update(int L,int R,int p) {
    if(x<=L&&R<=y) {
        tree[p]=k;
        return;
    }
    if(tree[p])tree[p<<1]=tree[p<<1|1]=tree[p],tree[p]=0;
    int mid=(L+R)>>1;
    if(x<mid)update(L,mid,p<<1);
    if(mid<y)update(mid,R,p<<1|1);
}
void Query(int L,int R,int p) {
    if(L+1==R) {
        vis[tree[p]]=1;
        return;
    }
    if(tree[p]){
        tree[p<<1]=tree[p<<1|1]=tree[p];
        tree[p]=0;
    }
    int mid=L+R>>1;
    Query(L,mid,p<<1);
    Query(mid,R,p<<1|1);
}
int main() {
    begin();
    Rd(n);
    Rd(l);
    for(int i=1; i<=n; i++){
        Rd(A[++top].x);
        A[top].n=i;
        Rd(A[++top].x);
        A[top].n=i+n;
    }
    sort(A+1,A+1+top);
    for(int i=1; i<=top; i++) {
        if(A[i].n>n)b[A[i].n-n]=cnt;
        else a[A[i].n]=cnt;
        if(A[i].x!=A[i+1].x)cnt++;
    }
    for(k=1; k<=n; k++){
        x=a[k];y=b[k];
        update(1,cnt,1);
    }
    int ans=0;
    Query(1,cnt,1);
    for(int i=1; i<=n; i++){
        if(vis[i])ans++;
    }
    printf("%d\n",ans);
    return 0;
}
```