# 陣列 Array
### Author : 極速車神大佬
###### tags: `MDCPP講義`

---

# 在上課開始之前，我們來分享一些東西

----

[APCS 6月報名](https://apcs.csie.ntnu.edu.tw/index.php/2022/04/20220413/)
從 4/22 開始報名 !
:::danger 
每次都會沒場次，真的要搶 
( 大概是開始5分鐘就會被搶光，而且包含進不去網站的時間
:::

----

:::info
下禮拜要模擬賽 !
還記得上次有每個人價值400元的獎品嗎 ?
範圍：~ 一維陣列 ( 今日上課範圍 )
:::

----

[YTP少年圖靈計畫](https://www.tw-ytp.com/)

[明道黑客松](https://www2.mingdao.edu.tw/hackathon/)

----

[APCS CAMP](https://apcs.camp/)

---

# 陣列起源

----

基本上你們可能會發現...
像是這個迴圈練習題 [超級瑪莉歐](http://mdcpp.mingdao.edu.tw/contest/29/problem/T11)
大家會不會想說，假如邪惡菇菇有超級多的話，我們不就要設超級多個變數?
這樣究竟可行嗎?

----

## 我們有沒有辦法將一群類似用途的變數歸類在一起 ?
## 這時候陣列就誕生了

----

## 讓我們來改寫 [超級瑪莉歐](http://mdcpp.mingdao.edu.tw/contest/29/problem/T11) 的程式碼吧 !

---

# 陣列簡介

----

陣列到底是什麼呢 ?
陣列也就代表著許多個相同型態的變數，歸類在一串稱作「陣列」的鏈裡面。
就好比說一條道路上每棟建築物都會有一個門牌，
那陣列的名字就像是道路的名字，陣列的索引值就代表門牌號碼，陣列的每個變數就代表每棟建築物的資訊。

----

宣告範例如下

```cpp=
int number[100];
```
第一個`int`代表的是這個**陣列的變數型態**，可以替換成`float`, `long long`, `double`, `bool`等等。

第二個`number`代表的是**陣列名稱**，可以替換成所有名字。

第三個`[100]`代表的是**陣列的大小**，也就是陣列有幾個變數，可以替換成任何數字。

----

其餘各種陣列宣告範例：
```cpp=
int age[500];
double score[500];
bool isgoodnumber[500];
```

----

## 那我們要怎麼使用呢 ?
## 只要利用以下方法：
```cpp=
int age[500];
age[0] = 15;
age[1] = 20;
age[2] = 454;
for(int i = 0; i < 3; i++) {
    cout << age[i] << ' ';
}
// Output: 15 20 454
```

----

## 不知道大家有沒有發現...
陣列的第一個位置是標記在 **[0]**。
這是由於電腦只有 0、1 ，所以在從二進位轉成十進位的時候，初始位置還是0！
:::danger
這是新手常犯的錯誤，大家需要注意一下。
:::


----

### 我知道陣列的宣告了，那我能不能一次把陣列的數字都先決定好，再開始做其他事情呢 ?
### 當然可以 !

----

我們需要將要初始化的東西放在一個大括號`{}`裡面，這稱作**建構式**。

```cpp
int age[5] = {1, 2, 3, 4, 5};

double score[3] = {2.19, 1.05};
// 在全域變數下，沒預設的會是 0
// 但在 main() 函數裡面宣告的話，會有奇奇怪怪的數字出現

float sum[10] = {};// 預設為0

bool check[3] = {true, false, true, false}; 
// 多出來的話，編譯器可以通過
// 就相當於多出來的變數初始宣告有跟沒有一樣

int num[] = {6, 5, 4, 3, 9};
// 陣列大小就是你初始的宣告大小
// 看起來很方便，實際很少用到
```

----

### 簡單範例：
現在有 $N$ 個數字，請輸出他們的總和。
$N \leq 50000$

```txt
範例輸入：
5
3 4 9 5 1
範例輸出：
22
```

(這題是可用陣列可不用的題目，為了方便理解)

----

以前你們大概的程式碼

```cpp=
#include <iostream>
using namespace std;
int main() {
    int n, sum = 0;
    cin >> n;
    for(int i = 0; i < n; i++) {
        int x;
        cin >> x;
        sum = sum + x;
    }
    cout << sum << endl;
}
```

----

可以換成這樣的寫法
```cpp=
#include <iostream>
using namespace std;
int main() {
    int number[50000], n, sum = 0;
    cin >> n;
    for(int i = 0; i < n; i++) {
        cin >> number[i];
    }
    for(int i = 0; i < n; i++) {
        sum = sum + number[i];
    }
    cout << sum << endl;
}
```

----

## 又不知道大家有沒有發現...
我們上面做了這件事情：
```cpp=
int number[50000];
```

那我們能不能
```cpp=
int n;
cin >> n;
int number[n];
```

----

答案是：在某些的 `C++` 版本中，可以
有些不行 (只接受常數)，所以盡量不要這麼做 !

----

### 簡單例題
[超級瑪莉歐進化版](http://mdcpp.mingdao.edu.tw/contest/29/problem/T15)
[簡單費氏數列](http://mdcpp.mingdao.edu.tw/problem/B001)
[找最大值](http://mdcpp.mingdao.edu.tw/problem/A009)
[資料分組](http://mdcpp.mingdao.edu.tw/problem/A031)

---

# C格式字串 / C格式字元陣列 / C++ STL string

----

不知道你們有沒有想過說
我能不能儲存一個人的名字 ?
這時候我們可以使用字串 !

----

但或許大家又會覺得，那標題寫「字串 / 字元陣列」又是因為什麼 ?
魔鬼藏在細節裡，讓我們繼續看下去。

----

有一句話說得好：
**「字串絕對是`char`類型陣列，但`char`類型陣列不一定是字串」**
一般我們直接宣告都是`char`類型陣列，那我們要怎麼宣告字串?

----

第一種 **(非常不優)**，未宣告大小的字元陣列
```cpp=
char c1[] = {'a', 'b', 'c'}; 
cout << c1 ; // abc + 亂碼
```
第二種 指定長度，後面元素沒有賦值的字元陣列
```cpp=
char c2[100] = {'a', 'b', 'c'};
cout << c2; // abc
```
第三種 不指定長度，後面加結束符 `'\0'` -> 字串
```cpp=
char c1[] = {'a', 'b', 'c' ,'\0'};
char c2[] = {'a', 'b', 'c', 0}; //直接寫0也可以
cout << c1; // abc
cout << c2; // abc
```
第四種 以`""`初始化，編譯器自動加 `'\0'`
```cpp=
char c2[] = "Hey there"; 
cout << c2; // Hey there
```
第五種 直接輸入，是一個字串 **(只有字串可以這樣用)**
```cpp=
char c1[100];
cin >> c1;
cout << c1;
```

----

註：提取單個字元的方式同一般陣列。

----

## 頗複雜的。( 講師也這麼認為 )
給上 [講師參考的連結](https://medium.com/andy%E7%9A%84%E8%B6%A3%E5%91%B3%E7%A8%8B%E5%BC%8F%E7%B7%B4%E5%8A%9F%E5%9D%8A/c%E8%AA%9E%E8%A8%80-01-%E5%AD%97%E5%85%83%E9%99%A3%E5%88%97-%E5%AD%97%E4%B8%B2%E5%82%BB%E5%82%BB%E5%88%86%E4%B8%8D%E6%B8%85%E6%A5%9A-45089f69f6be)
這大概只是寫`C`的人才會用到，又或者是追求極致效率的人。

----

講師是個佛系人物，也不希望記這些東西
所以我現在要講一個很棒的東西 !

----

## 先不要介紹一下 `C++ 標準函式庫 ( STL )`
歡迎參考 [算法班講義](https://hackmd.io/@CpiSWEDqSnq9qO6KplQraA/HkZt0-xVc#/)
我們現在要用到它裡面的一個東西，叫做`string`。

----

## 宣告方式
我們可以宣告整個 `string` 為一個變數 !

```cpp=
#include <iostream>
#include <string>
using namespace std;
int main() {
    string str;
    cin >> str;
    cout << str << endl;
    cout << str[5] << endl;
}
```
假如我們輸入 `Youzhe_is_a_minecraft master`
那就會輸出

```txt
Youzhe_is_a_minecraft master
e
```

----

字串練習題
[證書題 - 讀卡機](http://mdcpp.mingdao.edu.tw/contest/29/problem/T13)

---

本次回家練習題：

----


[內積計算](http://mdcpp.mingdao.edu.tw/contest/9/problem/A024)
[陣列反轉](http://mdcpp.mingdao.edu.tw/contest/9/problem/A022)
[電車載客數LV2](http://mdcpp.mingdao.edu.tw/problem/A022)

---

# 小技巧

---

## 小技巧1 - 陣列大小宣告

----

在宣告陣列大小時，我們說過盡量不要以變數來宣告陣列大小，那我們會有時候不小心發生 `Re (Runtime error)` 的情況，這是什麼意思呢 ?

舉[剛剛這個例子好了](https://hackmd.io/LQOdvQu-RsyMWZyfzRq70w?view#%E7%B0%A1%E5%96%AE%E7%AF%84%E4%BE%8B%EF%BC%9A)

----

假如我們程式碼寫成這樣 
( 與剛剛不同的是我們迴圈從$1$開始 )
```cpp=
#include <iostream>
using namespace std;
int main() {
    int number[50000], n, sum = 0;
    cin >> n;
    for(int i = 1; i <= n; i++) {
        cin >> number[i];
    }
    for(int i = 1; i <= n; i++) {
        sum = sum + number[i];
    }
    cout << sum << endl;
}
```

----

假如 $N=50000$，而我們有說陣列從 **[0]**  開始，那當迴圈裡面的數字 `i=50000`時，我們便會提取到 `number[50000]` ，而陣列只能取到`number[49999]`，這並不是合法的取值。

----

所以我們會常宣告成這樣：
```cpp=
int number[50005];
```
or
```cpp=
int number[50000 + 5];
```
or
```cpp=
int number[50000 + 50];
```
or
```cpp=
// 最常用
const int maxn = 50000 + 50; // 宣告此數字為一常數
int number[maxn];
```

---

## 小技巧2 - 輸入有空格的字串

----

:::info
我們都知道如果要輸入字串用 `cin` 即可
但有空格的話就不是這麼一回事
`cin`的情況下如果有空格，他會辨識為兩個字串，像是下面這樣：
( 這個情況在 `string`、`char[]`都會發生 )
:::


----

```cpp=
#include <iostream>
#include <string>
using namspace std;
int main() {
    string s1, s2, s3;
    cin >> s1 >> s2 >> s3;
    cout << s1 << endl;
    cout << s2 << endl;
    cout << s3 << endl;
}
```

----

```txt
輸入：
Hey there!
Timchen is a lolicon!
That's true!

錯誤的預期輸出：
Hey there!
Timchen is a lolicon!
That's true!

輸出：
Hey
there!
Timchen
```

----

那我們要怎麼避免呢 ?
若是C格式字串，我們可用 `cin.get(str, length), cin.getline(str, length)`
若是`string`，可用 `getline(cin, str)`
用法如下

----

### C 格式字串寫法
```cpp=
//cin.get(字串名稱, 要讀取的長度)
#include <iostream>
using namspace std;
int main() {
    char c1[100], c2[100], c3[100];
    cin.get(c1, 99), cin.get(c2, 99), cin.get(c3, 99);
    // 最後一個要放'\0'
    cout << c1 << endl;
    cout << c2 << endl;
    cout << c3 << endl;
}
```

----

### string 寫法
```cpp=
#include <iostream>
#include <string>
using namspace std;
int main() {
    string s1, s2, s3;
    getline(cin, s1), getline(cin, s2), getline(cin, s3);
    cout << s1 << endl;
    cout << s2 << endl;
    cout << s3 << endl;
}
```


---

## 小技巧3 - 提取 C格式字串 / string 長度

----

#### C格式字串的方法：
```cpp=
char c1[1000];
cin >> c1;
cout << strlen(c1) << endl; // 就是第一個字元到'\0'的長度
```

```txt
範例輸入：
Youzhe_is_so_smart

範例輸出：
18
```

----

#### string 寫法
```cpp=
string str;
cin >> str;
cout << str.size() << ' ' << str.length() << endl;
// 兩者皆可
```

```txt
範例輸入：
Youzhe_is_so_smart

範例輸出：
18 18
```

---

## 小技巧4 - string 用法

----

#### string 竟然可以相加 ? ( 不能相減、相乘、相除拉 )
```cpp=
string s1, s2;
cin >> s1 >> s2;
cout << s1 + s2 << endl;
```

```txt
範例輸入：
Youzhe_is_
so_smart

範例輸出：
Youzhe_is_so_smart
```

----

`string` 還有一些更進階的用法，歡迎參考 [這篇文章](https://clay-atlas.com/blog/2020/11/21/cpp-cn-stl-string/)

---

## 小技巧5 - 陣列大小限制

----

#### 可能有人會覺得，C++ 陣列這麼好用，我們是不是可以宣告無限大 ?

答案是否定的，這是因為他會有記憶體限制，從這裡看看：

----

![](https://i.imgur.com/7Jf7Dz2.png)

----

:::warning
右上角有個`Memory Limit`，這代表著他可以存多少量的東西，通常在`256MB, 512MB`左右的話都是 **總陣列長度最大在 $3\times10^7$ 的大小左右 ( 視不同系統而定 )**，這是要注意的地方 !
:::

---

# 謝謝大家 ~

