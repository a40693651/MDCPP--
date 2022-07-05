###### tags: `MDOI`

# DP Time

:coffee::coffee::coffee::coffee::coffee:


:coffee::coffee::coffee::coffee::coffee:

:tea::tea::tea::tea::tea:

優質DP入門講義：[[SA's DP]](https://hackmd.io/@sa072686/DP)

:tea::tea::tea::tea::tea:

---

## 前言

DP Time 是 DP 題單，這個題單的題目都是**樸素**DP。
樸素的意思是理論上不需要帶優化就可以解的出來了
(但是 LIS 的 BIT 太經典了)

---

## 0.1 看到DP怎麼下手

我也想知道QQ


## 0.2 線性DP

什麼叫做線性DP呢？其實就是最基本的DP
沒有特別分出來的東西都叫線性DP
所以說線性DP可能是遞推or遞迴or多維or其他阿撒布魯的
通常是簡單題( 難題也很多就是了(x )，但是不一定會直接裸裸的出現在題目裡
有時候會是在解題的過程中的一小部分
(如果硬要說的話前綴和也算一種DP(x 所以說前綴和也很重要 dayo!)

因為我相信你們都很會DP了，所以說我這邊就不負責任的不放題目了...(x
雖然我很想這麼說，但是練好線性DP才是進入後面恐怖東西的第一步
所以來刷題囉(以下題目可能有按難度分，沒有提示，就是大雜燴)

1. [[LG 1077]](https://www.luogu.com.cn/problem/P1077)
2. [[LG 1541]](https://www.luogu.com.cn/problem/P1541)
3. [[LG 4059]](https://www.luogu.com.cn/problem/P4059)
4. [[CF 474D]](https://codeforces.com/problemset/problem/474/D)
5. [[CF 118D]](https://codeforces.com/problemset/problem/118/D)
6. [[CF 607A]](https://codeforces.com/problemset/problem/607/A)
7. [[CF 225C]](https://codeforces.com/problemset/problem/225/C)
8. [[CF 543A]](https://codeforces.com/problemset/problem/543/A)
9. [[CF 711C]](https://codeforces.com/problemset/problem/711/C)
10. [[CF 1529D]](https://codeforces.com/contest/1529/problem/D)
11. [[UVA 1347]](https://vjudge.net/problem/UVA-1347) 經典題：兩相異路徑最短路

因為線性DP太多了，我隨便選幾題看起來不錯的就丟上來了
CF題來源大部分是這個題單 [[DP Practice]](https://vjudge.net/contest/424603)

## 1. LIS と LCS

### LIS 什麼的最喜歡了 >//<

LIS 就是一個二維偏序問題，套個 BIT 可以解決很多問題
但是也別忘記 LIS 原本的 DP 式了

1. [[裸題]](https://zerojudge.tw/ShowProblem?problemid=d242)
2. [[Almost 裸題]](https://zerojudge.tw/ShowProblem?problemid=f608)
3. [[拆最少 increasing sequence]](https://atcoder.jp/contests/abc134/tasks/abc134_e)
4. [[N維偏序]](http://domen111.github.io/UVa-Easy-Viewer/?103)
5. [[LIS變形1]](https://ac.nowcoder.com/acm/contest/11164/D?&headNav=acm)
6. [[LIS變形2]](https://codeforces.com/problemset/problem/1468/A)
7. [[LIS變形3]](https://codeforces.com/group/zrTK4HK8Ew/contest/296734/problem/A) (未解)

### LCS 什麼的最討厭了 OAO

1. [[裸題]](https://atcoder.jp/contests/dp/tasks/dp_f)
2. [[Edit Distance]](https://cses.fi/problemset/task/1639)
3. [[LCS變形1]](https://atcoder.jp/contests/abc130/tasks/abc130_e)
4. [[LCIS]](https://codeforces.com/problemset/problem/10/D)

### 聽說 LCS 可以轉 LIS ?

什麼意思? [[Almost 裸題]](https://zerojudge.tw/ShowProblem?problemid=f608) 是一個 LIS
如果我把 $x$ 座標換成 $a_i$， $y$ 座標換成 $b_i$ 
求 LCS 就變成跟那題求的東西一樣了 $\therefore LCS == LIS$ 

什麼時候可以用? 只需要輸出長度的時候
你說建圖也要 $NM$？數字小的時候可以Counting sort。數字大？離散化

複雜度？$O(Klog(min(N,M)) + R)$ 。$K$是數對數目， $N$ 和 $M$ 是序列長度，$R$是數字範圍。

最差情況下比 $O(NM)$ 還糟，但大部分時間快一點。$K$ 越小時可以用

1. [[UVA 10635]](https://vjudge.net/problem/UVA-10635)

---

## 2. 二維 DP

這邊的二維DP是在二維的平面上做DP，不是說狀態只有二維

1. [[裸 2 維路徑數 dp]](https://atcoder.jp/contests/dp/tasks/dp_h)
2. [[二維 dp]](https://atcoder.jp/contests/abc106/tasks/abc106_d)
3. [[最大子矩陣]](https://acm.timus.ru/problem.aspx?space=1&num=1146)
4. 還有很多但是我懶得找了，Atcoder上很多好題

---

## 3. 背包 DP

背包博大精深，千萬不要覺得他很簡單，難死

簡單分類：

* 0/1 背包
* 無限背包
* 有限背包
* 分組背包
* 樹上背包

先上裸題

1. [[0/1背包]](https://atcoder.jp/contests/dp/tasks/dp_d)
2. [[換位背包]](https://atcoder.jp/contests/dp/tasks/dp_e)
3. [[Bitset加速背包]](https://codeforces.com/contest/755/problem/F)
4. [[有限背包]](https://tioj.ck.tp.edu.tw/problems/1407)
有二進制拆分跟單調隊列優化兩種做法，如果不那麼在意效率的話寫二進制就好了。但是在某些題目可能還是會用到 (ex: Bitset加速背包那題可以用單調隊列優化輾過去)
5. [[分組背包]](https://www.luogu.com.cn/problem/P1064) 這是樹上背包的基礎
* 樹上背包 先等等 樹DP那邊再來

要注意的幾件事：

1. 背包是DP，不要硬套
2. 無限背包沒想好就會變成有限背包，要小心
3. 應該還有 但是我想不到

例題：
1. [[CF 336C]](https://codeforces.com/problemset/problem/366/C)
2. [[LG 1954]](https://www.luogu.com.cn/problem/P1941)
3. [[LG 1858]](https://www.luogu.com.cn/problem/P1858) 01背包前 $k$ 優解的價值和
4. [[CF 864E]](https://codeforces.com/problemset/problem/864/E) (未解)

## 4. 區間DP

在區間上做DP，通常複雜度都是 $N^2,N^3$
有時候可以搭配莫名其妙的四邊形優化

**用遞迴寫會異常好寫**

先來一些簡單經典題暖身

1. [[石子合併]](https://www.luogu.com.cn/problem/P1880) 這題最經典，但是要搭配斷環成鍊(也就是複製然後接兩倍)
2. [[n個矩陣相乘最少次數]](https://tioj.ck.tp.edu.tw/problems/1488)
3. [[最優三角剖分]](https://leetcode.com/problems/minimum-score-triangulation-of-polygon/)
4. [[105全國賽 pD]](https://tioj.ck.tp.edu.tw/problems/1914)

再來一些比較難一點點的經典好題

5. [[105全國賽pD變化]](https://vjudge.net/contest/400091#problem/H)
6. [[CF149D]](https://codeforces.com/problemset/problem/149/D) 特殊的轉移方式
7. [[IOI1998]Polygon](https://www.luogu.com.cn/problem/P4342) (未解)
8. [[顏色消除1]](https://codeforces.com/gym/102835/problem/E)
9. [[顏色消除2]](https://vjudge.net/problem/UVA-10559) (未解)

## 5. 環狀DP

如果解完石子合併的話你們應該學到了一個斷環成鍊的技巧了
但那個通常只有在區間DP可以用

正常的環狀DP作法是這樣子的：看哪裡有環，找環上一個點，枚舉他的所有Case，然後他就變成鍊了

環狀DP只是一個概念(技巧)而已，他不常裸裸的出現，所以說不放題目囉 OuO

其實是我懶(誤

## 6. 狀壓DP(位元DP)

貌似有人叫他位元DP，不要跟數位DP搞混了喔

### 6-1 $O(2^n)$

狀壓DP很常拿來把原本是 $N!$ 的複雜度壓成 $2^N$

大部分的做法就是用一個整數來表示一個狀態
令 $cnt(mask)$ = $mask$ 中 $1$ 的數量
最常見的手法是 $dp(mask)$ 代表前 $cnt(mask)$ 個人狀態是 $mask$ 的答案

上題目囉~

1. [[基本題]](https://atcoder.jp/contests/dp/tasks/dp_o)
2. [[UVa 11084]](https://onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=2025)
3. [[經典題]](https://cses.fi/problemset/task/1653)
4. [[LG 2704]](https://www.luogu.com.cn/problem/P2704) 題目簡單但細節頗多

### 6-2 $O(3^n)$ 枚舉子集的狀壓dp

這裡的 $3^n$ 不是指說用 $3$ 進制的整數存，一樣是二進制的整數當作狀態
最常見作法：先枚舉 $0\sim 2^n-1$，然後每一個再去做 dfs 枚舉子集
複雜度證明：$(2+1)^n=\sum\limits_{i=1}^{n}2^i\cdot$$n\choose i$

1. [[基本題]](https://atcoder.jp/contests/dp/tasks/dp_u)
2. [[LG 3959]](https://www.luogu.com.cn/problem/P3959) 按層轉移
3. [[CF1209 E2]](https://codeforces.com/problemset/problem/1209/E2) (未解)

### 5-3. 輪廓線DP

這是一個困難的DP，我不太會，但是他蠻有趣的
他其實算是一種狀壓DP的分支，但又不完全是

## 6. 樹DP

這是一個恐怖的章節，因為我不會樹DP
樹DP比背包還要博大精深，他自己一個DP就延伸出很多分支了
但也因為這樣，他非常重要，可以說是DP的非常大個章節

主要有以下分支：

1. 普通DP
2. 樹上背包
3. 換根DP
4. 基環樹(只有一個環的樹)
5. 其他毒瘤(虛樹、長鍊剖分)

下面是一些 MISC 的題目，主要去看洛谷題單

1. [[換根DP]](https://cses.fi/problemset/task/1132)
2. [[好好寫就是 $O(n^2)$ 樹 dp]](https://acm.timus.ru/problem.aspx?space=1&num=1018)
3. [[TOI 2020 pB]](https://tioj.ck.tp.edu.tw/problems/2189)
4. [[TOI 2020 pB 推廣題]](https://codeforces.com/group/zrTK4HK8Ew/contest/296734/problem/C)

題單：[[洛谷樹DP]](https://www.luogu.com.cn/training/13994#problems)

