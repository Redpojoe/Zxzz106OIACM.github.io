---
layout: default
title: "快速IO"
date: 2018-01-01
category: Template
tags: [模板,水分利器]
---

# 快速IO

<p align="right">小C叫它们读入输出挂</p>

## 快速输入

```C++
void Rd(int &res) {
    char c;
    res=0;
    int flag=1;
    while(c=getchar(),c<48) {
        if(c=='-')flag=-1;
    }
    do res=(res<<3)+(res<<1)+(c^48);
    while(c=getchar(),c>=48);
    res*=flag;
}
```

## 快速输出

```C++
void Pdfs(int n) {
    if(n==0)return;
    Pdfs(n/10);
    putchar(n%10^48);
}
void Print(int n) {
    if(n<0) {
        putchar('-');
        n=-n;
    }
    if(n==0)putchar('0');
    else Pdfs(n);
}
```

## 超快速IO

```C++
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
```

<b><font color="red">[注意]：</font></b>
1. begin() 要记得放到main()的第一行  
2. 注意MT的大小