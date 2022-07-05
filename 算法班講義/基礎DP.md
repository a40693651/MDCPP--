---
type: slide
---
# dp

---

## 淺談dp

----

## Dynamic Programming
一個抽象的概念

----

### 用途
* 壓縮空間
* 壓縮時間

----

## 樸素dp

----

線性dp 二維dp LCS LIS 
背包dp 區間dp 狀壓dp 樹dp
...

----

## 進階dp

----

單調隊列優化、斜率優化、凸包...

---

## 基本概念
**費氏數列**
$f(n)=f(n-1)+f(n-2)$

----

```cpp=
int f(int n)
{
    if (n == 0)
        return 1;
    if (n == 1)
        return 1;
    return f(n - 1) + f(n - 2);
}
    
```

----

![](https://i.imgur.com/R6GwlTH.png)
用遞迴會產生非必要計算

----

```cpp=
dp[0] = dp[1] = 1;
int f(int n)
{
    if (dp[n])
        return dp[n];
    return dp[n] = f(n - 1) + f(n - 2);
}
```

----

若我們將計算結果儲存下來，則會剩下這樣：
![](https://i.imgur.com/aTPX2VF.png)

----

### 實做dp
* 觀察題目的複雜度
* 開dp陣列並賦予其狀態、意義
* 初始化
* 轉移


----

```cpp=
//一般遞迴式
int f(int n)
{
    if (n == 0)
        return 1;
    if (n == 1)
        return 1;
    return f(n - 1) + f(n - 2);
}
//dp
int dp[n];//宣告陣列，賦予意義
dp[0] = dp[1] = 1;//初始化
int f(int n)
{
    if (dp[n])
        return dp[n];
    return dp[n] = f(n - 1) + f(n - 2);//轉移式
}
```

----


#### Top-down
```cpp=
dp[0] = dp[1] = 1;
int f(int n)
{
    if (dp[n])
        return dp[n];
    return dp[n] = f(n - 1) + f(n - 2);
}
```

----

#### Bottom-up
```cpp=
dp[0] = dp[1] = 1;
for (int i = 2; i <= n; i++)
    dp[i] = dp[i - 1] + dp[i - 2];
```

----

## 遞迴vs.迴圈

----

## 遞迴
- 直觀
- 正確率較高
- 費時

----

## 迴圈
- 後期較複雜
- 確定性

----

## 題目類型
- 計數型
- 最佳化型

----

#### 標記
```cpp=
cnt++;
used[i] = 1;

int f(int n)
{
    if (used[n])
        return dp[n];
    used[n] = 1;
    return dp[n] = f(n - 1) + f(n - 2);
}
```

---

## 線性dp
所有dp的基礎

----

### 爬樓梯之問題一、二、三
http://mdcpp.mingdao.edu.tw/problem/A048
http://mdcpp.mingdao.edu.tw/problem/A049
http://mdcpp.mingdao.edu.tw/problem/A050

----

### Coin Combinations I
https://cses.fi/problemset/task/1635


----

### Coin Combinations II
https://cses.fi/problemset/task/1636

---

## 想法題

----

## Money Sums
https://cses.fi/problemset/task/1745

----

## Counting Towers
https://cses.fi/problemset/task/2413

---

## 二維dp

----

給定一個$n*m$的棋盤
起始點位於左上角$(1,1)$
每次僅能向右向下一單位
問由起點$(1,1)$到終點$(n,m)$
的路徑數

----

- $dp[i][j]$表由起點至$(i,j)$的方法數

每個點(邊界除外)
皆可從其上方及左方抵達

----

$dp[i][j] = dp[i - 1][j] + dp[i][j - 1]$

----

* 邊界初始化
* 以座標去宣告dp


----

## Grid Paths
https://cses.fi/problemset/task/1638

----

## 採果實問題
http://mdcpp.mingdao.edu.tw/problem/A052

---

## LCS

----

### Longest Common Subsequence

給定兩個序列$S,T$
在這兩序列中挑選共同的字元
組成一個新序列
使這個序列之長度最長

----

$S= {4,6,2,3,1,7}$
$T={6,5,3,7,1}$
$LCS(S,T)=6,3,1or6,3,7$

----

```cpp=
//dp[i][j]表示LCS(s[0 ~ i], t[0 ~ j])
if(s[i] == t[j])    
    dp[i][j] = dp[i - 1][j - 1] + 1;
else
    dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
```

----

![](https://i.imgur.com/8TxgkuE.png)

----

## Edit Distance
https://cses.fi/problemset/task/1639

---

## LIS

----

### Longest Increasing Subsequence

在一個字串之中
照順序從字串選取元素
組成一個呈嚴格遞增的序列

----

$S=7, 3, 5, 3 ,6 ,2, 9, 8$

$LIS=4$

----

先假設有一個字串$1,9,7$
接著我們找出兩個序列
$1,9$和$1,7$
我們發現第二個元素是$7$的話
後面所能接續的字串更有潛力

----

因此我們將情況統整一下
可以得到兩個case

----

字串中的元素 > $LIS$最後元素
$LIS$長度+1

反之
選擇更富有潛力的元素

----

$S=7, 3, 5, 3 ,6 ,2, 9, 8$



| 地$i$個元素| LIS長度| LIS |
| -------- | -------- | -------- |
|1|1|7|
|2|1|3|
|3|2|3 5|
|4|2|3 5|
|5|3|3 5 6|
|6|3|2 5 6|
|7|4|2 5 6 9|
|8|4|2 5 6 8|

----

在存取$LIS$時
若以線性的方式去比大小
容易吃$TLE$
- 時間複雜度：$O(nL)$

----

我們可以利用二分搜
去尋找取代元素的值
如此一來以必免吃$TLE$

* 時間複雜度：$O(nlogL)$

----

用vector存取LIS
以lower_bound()查找取代值


----

## Increasing Subsequence
https://cses.fi/problemset/task/1145
