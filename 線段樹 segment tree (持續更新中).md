# 線段樹 segment tree (持續更新中)
## 用途
我們常常會遇到區間問題，像是這題 [動態區間總和](https://cses.fi/problemset/task/1648)
當我們在遇到靜態區間總和，我們可以用**前綴和**進行O(1)的詢問
但遇到修改就無法進行O(1)查詢，那我們勢必要利用新的資料結構 / 演算法了
那就是什麼？
### 線段樹 !
---
圖片取自 [這裡](https://daydaynews.cc/technology/322763.html)
![](https://i.imgur.com/EpsteIn.png)
看到這裡，應該知道它為什麼叫做線段樹了
從上圖可以發現，最上層是1~4的線段，而往下會分別分成兩半，一直到分成一個
而每個線段會儲存該點的資訊，資訊是什麼就視情況而定

---
### 用途

仔細發現，1~4 的區間和就會是 1~2 的區間和加上 3~4 的區間和
線段樹也就是利用向下分支的特性，來達成儲存線段的目的
而在每個節點會代表著那個線段的總和。
而在查詢的時候，我們只要向下遞迴，並且進行下列兩項事情
當前線段是$(l,r)$時，要查詢(L,R)
1. 如果$L<=l、R>=r$，也就是目前線段完全被查詢範圍覆蓋，回傳此線段資訊，並不用執行2~4步驟
2. 若$L<=mid$，向左遞迴並且合併答案
3. 若$R>mid$，向右遞迴並且合併答案
4. 回傳答案
---

### 修改

跟查詢一樣，我們只要一直遞迴，並且將該節點進行修改，最後向上合併即可

---

### 如何儲存?

我們可以將最上層的節點編號1，向左子節點乘上2，右子節點乘上2加上1，會發現不會重複，並且最大值不會高過於 $4*n$

## 單點改值，區間和範例CODE
:::spoiler CODE
``` cpp=
#include <bits/stdc++.h>
#define i1 (i<<1)
#define i2 (i<<1|1)
#define mid ((l+r)>>1)

// val[]為當前線段所儲存的線段總和
// i為節點編號，l,r為當前線段左右界，p為要更新的節點，v為要更新的數字
// void init()可寫可不寫，可換成modify使用n次
// arr[]為初始數字

int arr[maxn],val[4*maxn];
//要開4倍大小，不然會RE或MLE，因為完全二元樹會可以開2*n，但是線段樹不完全是
void init(int l,int r,int i) {
    //void init() 複雜度 O(nlogn)
    if(l==r) {
        val[i]=arr[l];
        return ;
    }
    init(l,mid,i1);
    init(mid+1,r,i2);
    val[i]=val[i1]+val[i2];
}

void modify(int l,int r,int p,int i,int v) {
    //void modify() 複雜度 O(logn)
    if(l==r) {
        val[i]=v;
        return ;
    }
    if(p<=mid) modify(l,mid,p,i1,v);//如果要修改的點在左子樹
    else modify (mid+1,r,p,i2,v);//如果要修改的點在右子樹
    val[i]=val[i1]+val[i2]; //很重要，不然你的數字就不會是下面兩項的和
}

int query(int l,int r,int L,int R,int i) {
    //int query() 複雜度 O(logn)
    if(L<=l and R>=r) return val[i]; //整個線段都是你要的值，就回傳
    int sum=0;
    if(L<=mid) sum+=query(l,mid,L,R,i1);
    if(R>mid) sum+=query(mid+1,r,L,R,i2);
    return sum;
}
```
:::
## 複雜度

void init()的部分，可以看出線段樹是一個接近二元樹，而將二元樹跑滿的複雜度：
$n(1/n+2/n+3/n+......n/n) = 2n-1$
複雜度 $O(n)$

void modify() 的部分，由於需要往下跑找到需要節點，而線段樹層數為 $logn$
複雜度 $O(logn)$

int query()的部分，透過二分的方法，最多需要遍歷 $4* logn$ 個節點左右
複雜度 $O(logn)$

---

## 單點修改例題
[區間最小值](https://cses.fi/problemset/task/1649)

[線段樹二分](https://cses.fi/problemset/task/1143/)

[區間相異元素各數](https://cses.fi/problemset/task/1734)

## 區間修改線段樹

你以為自己會了線段樹了嗎!!!
並沒有。
像是這題[這裡](https://cses.fi/problemset/task/1651)遇到多點修改的話，前面有提到void modify()複雜度為$O(logn)$
難道要全部這樣修改$O(nlogn)嗎 ? 這樣還比前綴和還爛(X

---

## lazy tag

救星來了~
我們可以用與void query()類似的寫法，只要整個線段都是更新的範圍，這時候就把這個位置的lazy tag放在這裡，並且同時更新這個位置的值。
這麼做是因為這個lazy tag代表以下的節點尚未更新，要用lazy tag更新
接著，每當遇到有lazy tag的點，就將這個點的lazy tag下傳，如此一來下方的節點才會是對的，並且移除原本的lazy tag。
總述以上：
1. 有lazy tag代表這個點以下還沒被更新，需要下傳
2. 賦予lazy tag是在當前線段完全都需要更新時，之後就可以不用遞迴

## 區間加值，查詢區間和code
:::spoiler CODE
```cpp=
#include <bits/stdc++.h>
#define i1 (i<<1)
#define i2 (i<<1|1)
#define mid ((l+r)>>1)

// val[]為當前線段所儲存的線段總和
// i為節點編號，l,r為當前線段左右界，p為要更新的節點，v為要更新的數字
// void init()可寫可不寫，可換成modify使用n次
// arr[]為初始數字

int arr[maxn],val[4*maxn],lazy[4*maxn];
//要開4倍大小，不然會RE或MLE，因為完全二元樹會可以開2*n，但是線段樹不完全是
void init(int l,int r,int i) {
    //void init() 複雜度 O(n)
    if(l==r) {
        val[i]=arr[l];
        lazy[i]=0;
        //有時候lazy[i]不能初始為0，反正就自己找一個數字代表沒有lazy tag
        return ;
    }
    init(l,mid,i1);
    init(mid+1,r,i2);
    val[i]=val[i1]+val[i2];
}

//lazy tag下傳
inline void pushdown(int l,int r,int i) {
    if(lazy[i]) {
        lazy[i1]+=lazy[i];
        lazy[i2]+=lazy[i];
        val[i1]+=lazy[i]*(mid-l+1);
        val[i2]+=lazy[i]*(r-mid+1);
        lazy[i]=0;
    }
}
void modify(int l,int r,int L,int R,int i,int v) {
    //void modify() 複雜度 O(logn)
    if(L<=l and R>=r) {
        val[i]+=v*(r-l+1);
        lazy[i]+=v;
        return ;
    }
    pushdown(l,r,i);
    if(L<=mid) modify(l,mid,L,R,i1,v);//如果要修改的點在左子樹
    if(R>mid) modify(mid+1,r,L,R,i2,v);//如果要修改的點在右子樹
    val[i]=val[i1]+val[i2]; //很重要，不然你的數字就不會是下面兩項的和
}

int query(int l,int r,int L,int R,int i) {
    //int query() 複雜度 O(logn)
    if(L<=l and R>=r) return val[i]; //整個線段都是你要的值，就回傳
    pushdown(l,r,i);
    int sum=0;
    if(L<=mid) sum+=query(l,mid,L,R,i1);
    if(R>mid) sum+=query(mid+1,r,L,R,i2);
    return sum;
}
```
:::

## 區間修改例題

[經典題](https://cses.fi/problemset/task/2166)

[經典題](https://codeforces.com/contest/1555/problem/E)

[矩形覆蓋面積](https://tioj.ck.tp.edu.tw/problems/1224)

[區間改值、加值](https://cses.fi/problemset/task/1651)

## 指標線段樹
### 區間加值，查詢區間和code
這是一種用指標代替id的方法，空間消耗會比較小
:::spoiler CODE
```cpp=
#include <bits/stdc++.h>
#define mid ((l+r)>>1)
using namespace std;
struct Node{
    int val,lazy;
    Node *lc,*rc;
    Node(){
        val=lazy=0,lc=rc=NULL;
    }
    void pushdown(int l,int r) {
        if(lazy) {
            lc->lazy+=lazy;
            rc->lazy+=lazy;
            lc->val+=(mid-l+1);
            rc->val+=(r-mid);
            lazy=0;
        }
    }
}
Node* init(int l,int r) {
    Node* node=new Node();
    if(l==r) {
        node->val=arr[l];
        return node;
    }
    node->lc=init(l,mid);
    node->rc=init(mid+1,r);
    node->val=node->lc->val+node->rc->val;
}
void modify(Node* node,int l,int r,int L,int R,int v) {
    if(L<=l and R>=r) {
        node->val+=v*(r-l+1);
        node->lazy+=v;
        return ;
    }
    node->pushdown(l,r);
    if(L<=mid) modify(node->lc,l,mid,L,R,v);
    if(R>mid) modify(node->rc,mid+1,r,L,R,v);
    node->val=node->lc->val+node->rc->val;
}
void query(Node* node,int l,int r,int L,int R,int v) {
    if(L<=l and R>=r) {
        node->val+=v*(r-l+1);
        node->lazy+=v;
        return ;
    }
    node->pushdown(l,r);
    int sum=0;
    if(L<=mid) sum+=query(node->lc,l,mid,L,R,v);
    if(R>mid) sum+=query(node->rc,mid+1,r,L,R,v);
    return sum;
}
```
:::
## 動態開點線段樹

有時候我們線段樹需要的範圍很大，但是Queries卻不多時，我們就可以考慮動態開點線段樹。
動態開點就是將點用到的時候再把它開出來，線段樹每次用到的點只會有 $logn$，進而將空間複雜度降至 $qlogn$

我發現我好像沒有純模板(其實只是因為只寫過兩題
[CF 803G](https://codeforces.com/contest/803/problem/G)

[TOI 2021 1 pD](http://mdcpp.mingdao.edu.tw/problem/TOI_2021_1_pD)
:::spoiler CODE
```cpp=
#include <bits/stdc++.h>
#define pb push_back
#define pii pair<int,int>
#define tup tuple<int,int,int>
#define g0 get<0>(i)
#define g1 get<1>(i)
#define g2 get<2>(i)
#define f first
#define s second
#define lowbit(x) (x&-x)
#define endl '\n'
#define m ((l+r)>>1)
#define i1 (i<<1)
#define i2 (i1+1)
using namespace std;
const int maxn = 2e5 + 5 ;
int st[maxn][20],n,k,q;
int stquery(int l,int r)
{
	if(r-l+1>=n) return min(st[1][int(log2(n))],st[n-(1<<(int(log2(n))))+1][int(log2(n))]);
	if(l%n!=0) l%=n;
	else l=n;
	if(r%n!=0) r%=n;
	else r=n;
	if(l<=r)
	{
		int x=log2(r-l+1);
		return min({st[l][x],st[r-(1<<x)+1][x]});
	}
	else
	{
		int x=log2(n-l+1),y=log2(r);
		return min({st[1][y],st[r-(1<<y)+1][y],st[l][x],st[n-(1<<x)+1][x]});
	}
}
struct Node
{
	int val,lazy;
	Node *lc,*rc;
	Node(){val=lazy=0;lc=rc=NULL;}
	void pushup(int l,int r)
	{
		int a=lc->val,b=rc->val;
		if(a==0) a=stquery(l,m);
		if(b==0) b=stquery(m+1,r);
		val=min(a,b);
	}
};
void stinit()
{
	for(int j=1;j<=19;j++)
	{
		for(int i=1;i<=n;i++)
		{
			if(i+(1<<j)-1>n) break;
			st[i][j]=min(st[i+(1<<(j-1))][j-1],st[i][j-1]);
		}
	}
}
void pushdown(Node* node)
{
	node->lc->val=node->lc->lazy=node->lazy;
	node->rc->val=node->rc->lazy=node->lazy;
	node->lazy=0;
}
void upt(Node* node,int l,int r,int L,int R,int v)
{
	if(L<=l and R>=r) 
	{
		node->val=node->lazy=v;
		return ;
	}
	if(node->lc==NULL) node->lc=new Node();
	if(node->rc==NULL) node->rc=new Node();
	if(node->lazy) pushdown(node);
	if(L<=m) upt(node->lc,l,m,L,R,v);
	if(R>m) upt(node->rc,m+1,r,L,R,v);
	node->pushup(l,r);
}
int query(Node* node,int l,int r,int L,int R)
{
	if(L<=l and R>=r)
	{
		if(node->val==0) return stquery(l,r);
		else return node->val;
	}
	if(node->lc==NULL) node->lc=new Node();
	if(node->rc==NULL) node->rc=new Node();
	if(node->lazy) pushdown(node);
	int a=1e9,b=1e9;
	if(L<=m)
	{
		if(node->lc->val==0) a=stquery(L,min(m,R));
		else a=query(node->lc,l,m,L,R);
	}
	if(R>m)
	{
		if(node->rc->val==0) b=stquery(max(L,m+1),R);
		else b=query(node->rc,m+1,r,L,R);
	}
	return min(a,b);
}
signed main()
{
	cin>>n>>k;
	for(int i=1;i<=n;i++) cin>>st[i][0];
	stinit();
	cin>>q;
	Node* root=new Node();
	while(q--)
	{
		int x,l,r,v;
		cin>>x;
		if(x==1) cin>>l>>r>>v,upt(root,1,n*k,l,r,v);
		else cin>>l>>r,cout<<query(root,1,n*k,l,r)<<endl;
	}
}
```
:::


## 可持久化線段樹

可持久化線段樹就是利用動態開點的特性，將線段樹從節點複製一次，存下個個複製版本後就可以處理各個版本的問題。
我只寫過極上裸題

[CSES 1737](https://cses.fi/problemset/task/1737)
:::spoiler CODE
```cpp=
#include <bits/stdc++.h>
#define pb push_back
#define pii pair<int,int>
#define tup tuple<int,int,int>
#define g0 get<0>(i)
#define g1 get<1>(i)
#define g2 get<2>(i)
#define f first
#define s second
#define lowbit(x) (x&-x)
#define endl '\n'
#define m ((l+r)>>1)
#define i1 (i<<1)
#define i2 (i1+1)
#define int long long
using namespace std;
struct Node
{
	int val;
	Node *lc,*rc;
	Node(){val=0,lc=rc=NULL;}
	void pushup(){val=lc->val+rc->val;}
};
const int maxn = 2e5 + 5 ;
int num[maxn];
Node* root[maxn];
void build(Node* node,int l,int r)
{
	if(l==r) 
	{
		node->val=num[l];
		return ;
	}
	node->lc=new Node();
	node->rc=new Node();
	build(node->lc,l,m);
	build(node->rc,m+1,r);
	node->pushup();
}
Node* copy(Node* node)
{
	Node* nd=new Node();
	nd->val=node->val;
	nd->lc=node->lc;
	nd->rc=node->rc;
	return nd;
}
void upt(Node* node,int l,int r,int p,int v)
{
	if(l==r and r==p) 
	{
		node->val=v;
		return ;
	}
	if(p<=m)
	{
		node->lc=copy(node->lc);
		upt(node->lc,l,m,p,v);
	}
	else 
	{
		node->rc=copy(node->rc);
		upt(node->rc,m+1,r,p,v);
	}
	node->pushup();
}
int query(Node* node,int l,int r,int L,int R)
{
	if(L<=l and R>=r) return node->val;
	int ans=0;
	if(L<=m) ans+=query(node->lc,l,m,L,R);
	if(R>m) ans+=query(node->rc,m+1,r,L,R);
	return ans;
}
signed main()
{
	ios::sync_with_stdio(0);
	cin.tie(0);
	int n,q,pos=1;
	cin>>n>>q;
	root[1]=new Node();
	for(int i=1;i<=n;i++) cin>>num[i];
	build(root[1],1,n);
	while(q--)
	{
		int a,k,l,r;
		cin>>a;
		if(a==3) cin>>k,root[++pos]=copy(root[k]);
		if(a==2)
		{
			cin>>k>>l>>r;
			cout<<query(root[k],1,n,l,r)<<endl;
		}
		if(a==1)
		{
			cin>>k>>l>>r;
			upt(root[k],1,n,l,r);
		}
	}
}
```
:::

## 題目


