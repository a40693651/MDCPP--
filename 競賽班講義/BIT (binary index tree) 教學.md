---
title: BIT (binary index tree) 教學

---

# BIT (binary index tree) 教學

---

## 簡介

Binary index tree，( 以下簡稱 Bit，不要與 binary search tree (Bst) 搞混 )，也被稱作 Fenwick Tree，是一個在線段樹之後被發明，拿來取代線段樹的部分功能的工具。
相較於線段樹，BIT 的寫法簡單，不需要遞迴，是一個常在競賽中發揮的工具。

---

## 架構

----

![](https://robert1003.github.io/assets/images/fenwick-tree/bit.png)

取自 [這裡](https://robert1003.github.io/assets/images/fenwick-tree/bit.png)

----

Bit 的架構是建立於二進制數字的一個特性**lowbit**上，而什麼是 **lowbit** 呢 ?
lowbit 代表的是數字二進制表示的「最右側的 1 所代表的大小」，
如：
$34$ 的二進制為 $(100010)_2$，而最右側的 $1$ 是在第 2 個位置，$2^{2-1}=2$，故 **lowbit(34)=2**。
同理，$4$ 的二進制為 $(100)_2$，而最右側的 $1$ 是在第 3 個位置，$2^{3-1}=1$，故 **lowbit(4)=4**。

----

這樣做有什麼好處呢 ? 我們可以設一個陣列叫做 $bit[]$，而 $bit[x]$ 代表著 $arr[x - lowbit(x) + 1]$ 到 $arr[x]$。
我們其實可以發現，我們若要求 $arr[1]$ 到 $arr[x]$ 的總和，那只要把 $x$ 的二進制的 $1$ 全部加起來就可以了 !

----

## 使用

----

在線段樹我們常用到 $build$ 函式，但通常因為 Bit 常數小，我們更常用 $N$ 次複雜度$O(logN)$ 的修改

----

### lowbit

若直接依照定義進行 $lowbit$ 的建立，複雜度為 $O(logN)$，
但我們可以利用補數的特性，將一個數字取補數後，在原本最右邊都是 $0$ 的幾位都變成 $0$，而在 $+1$ 之後，都會變成 $1$，且 $lowbit$ 那位會變成 $1$，取位元 $and$ 即可。
如：
$34=(100010)_2$
$\sim34=(011101)_2$
$\sim34+1=(011110)_2$
$(34) \& (\sim34+1)=(000010)_2$

又因負數在電腦的表示就是補數加 $1$，故也可以寫成原數與補數取位元 $and$

以下是範例：
```cpp=
int lowbit(x) {
    return (~x + 1) & x;
    // 或
    return (-x) & x;
}
```

我們也常常將他 define：

```cpp=
#define lowbit(x) (x & -x)
```

複雜度 $O(1)$

----

### 單點修改

BIT 的單點修改很簡單，就是從要修改的位置往上加 $lowbit$ 即可。
可以發現往上加 $lowbit$ 就能回到上層有被覆蓋的陣列裡面

```cpp=
void add(int p, int v) {
    while(p <= n) {
        bit[p] += v;
        p += lowbit(p);
    }
}
```

複雜度 $O(logN)$

----

### 前綴查詢

前面有提到 Bit 就是利用位元為 1 的位置加總而成，故我們可以每次減 $lowbit$ 並加總即可

```cpp=
int cal(int p) {
    int ret = 0;
    while(p > 0) {
        ret += bit[p];
        p -= lowbit(p);
    }
    return ret;
}
```

----

### 區間查詢

線段樹的查詢是一個前綴查詢，故我們如果要進行區間查詢的話，我們是利用扣除的方式，以查詢區間和為例：

```cpp=
void sum(int l, int r) {
    return cal(r) - cal(l - 1);
}
```

可以發現，相較於線段樹，Bit 能處理的只有「可悔改」的操作，也就是能透過扣除的方式得來的資訊，故區間最大、最小等等都是不能用一般的 Bit 完成的，但如果是像 $LIS$ 一樣，查詢前綴最大值，Bit 是可以被使用的

----

### 區間修改

線段樹可以輕鬆地做到區間修改的動作，但是 Bit 若要區間修改，需要建立兩個 Bit，而比較麻煩，通常也可以利用線段樹直接完成，通常不會用到。
有興趣可以參考下面的講義

---


## 例題

1. [逆序數對](https://tioj.ck.tp.edu.tw/problems/1080)
2. [LIS](https://tioj.ck.tp.edu.tw/problems/1175)
3. [區間查詢](https://cses.fi/problemset/task/1648)
4. [活用](https://atcoder.jp/contests/abc253/tasks/abc253_f)

---

## 小結

----

雖然 Bit 看似一個被弱化的線段樹，但其因為常數極小，且撰寫方便，常常被利用在競賽中，練好這個能夠寫完很多區間問題相關題目 !

---



## 更多資源

----

[樹狀數組黑科技講義](http://magolor.cn/2018/08/27/2018-08-27-blog-01/#%E5%89%8D%E8%A8%80)

----
