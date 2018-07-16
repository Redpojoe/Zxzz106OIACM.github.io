---
layout: default
---

# Test

### 线段树模板

```C++
#include<stdio.h>
#include<string.h>
#define M 100005
#define LL long long
LL data[M],sum[M];
struct node {
	int L,R;
	LL add,sum; 
} tree[M*4];
void Build(int L,int R,int p) {
	tree[p].L=L,tree[p].R=R;
	tree[p].sum=tree[p].add=0;
	if(L==R)return;
	int mid=(L+R)>>1;
	Build(L,mid,2*p);
	Build(mid+1,R,2*p+1);
}
void Up(int p) {
	tree[p].sum=tree[2*p].sum+tree[2*p+1].sum;
}
void Down(int p) {
	if(tree[p].add==0)return;
	tree[2*p].sum+=tree[p].add*(tree[2*p].R-tree[2*p].L+1);
	tree[2*p].add+=tree[p].add;
	tree[2*p+1].sum+=tree[p].add*(tree[2*p+1].R-tree[2*p+1].L+1);
	tree[2*p+1].add+=tree[p].add;
	tree[p].add=0;
}
void Update(int L,int R,LL add,int p) {
	if(tree[p].L==L&&tree[p].R==R) {
		tree[p].sum+=(R-L+1)*add;
		tree[p].add+=add;
		return;
	}
	Down(p);
	int mid=(tree[p].L+tree[p].R)>>1;
	if(mid>=R)Update(L,R,add,2*p);
	else if(mid<L)Update(L,R,add,2*p+1);
	else {
		Update(L,mid,add,2*p);
		Update(mid+1,R,add,2*p+1);
	}
	Up(p);
}
LL Query(int L,int R,int p) {
	if(tree[p].L==L&&tree[p].R==R) {
		return tree[p].sum;
	}
	Down(p);
	int mid=(tree[p].L+tree[p].R)>>1;
	if(R<=mid)return Query(L,R,2*p);
	else if(L>mid)return Query(L,R,2*p+1);
	else  return Query(L,mid,2*p)+Query(mid+1,R,2*p+1);
}
int main() {
	int n,m,a,b,i;
	LL c;
	char str[10];
	while(scanf("%d %d",&n,&m)!=EOF) {
		Build(1,n,1);
		sum[0]=0;
		for( i=1; i<=n; i++) {
			scanf("%lld",&data[i]);
			sum[i]=sum[i-1]+data[i];
		}
		while(m--&&scanf("%s %d %d",str,&a,&b)) {
			if(str[0]=='Q') {
				printf("%lld\n",sum[b]-sum[a-1]+Query(a,b,1));
			} else {
				scanf("%lld",&c);
				Update(a,b,c,1);
			}
		}
	}
	return 0;
}
```