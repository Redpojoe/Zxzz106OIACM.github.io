---
layout: default
title: "Billboard"
date: 2018-07-17
category: Segment Tree
tags: [线段树]
---

# 线段树专题

## Billboard

[题目链接](https://cn.vjudge.net/problem/HDU-2795#author=Purity)  

在一个h*w的海报墙上贴高为1，宽为wi的海报

1. 优先选择最上面的位置  
2. 在所有最上面的可能位置中，他会选择最左面的位置
3. 不能把已经贴好的海报盖住并且不能超出海报墙的范围

对于每张海报，输出它被贴在第几行(顶部是第一行)  
如果某张海报贴不下了，则输出-1  

## 思路

>利用线段树，查询区间最大值

结构体

```C++
struct node{
    int L,R;
    int max;
}tree[M<<2];
```

&emsp;其中max表示区间内有最多空位那一行的空位长度。对每张海报，若左子树满足则查询左子树，否则查询右子树

```C++
void Query(int x,int p) {
	if(tree[p].L==tree[p].R) {
		printf("%d\n",tree[p].L);
		tree[p].max-=x;
		return;
	}
	if(x<=tree[p<<1].max)
		Query(x,p<<1);
	else
		Query(x,p<<1|1);
	up(p);
}
```

>其实如果想对线段树查询的对象其余的都是套路了