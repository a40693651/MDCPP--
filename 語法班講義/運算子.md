# MDCPP 校內培訓講義 -- 運算子

----

### 大家先登入 Google Classroom 看今天的講義
### 也登入 MDjudge 帳號 
### 帳號和密碼都是學號六碼

----

### 只有不到10個人寫作業...
![](https://i.imgur.com/85SFA01.png)

---

### 我一開始也認為會了就不需要練習
### 其實打程式最忌諱的就是
### 不常打程式 !!!

----

### 在第十周我們有舉辦APCS模擬賽 (基礎組、進階組分開
### 會有排名，也有獎品
### 所以記得練習拉 ~

----

### 讓我們先來複習一下上次的東西...

---

### C++ 基礎架構
```cpp=
#include<iostream>
using namespace std;
int main(){
    
}
```

----

### cout 輸出
```cpp=
#include<iostream>
using namespace std;
int main(){
    cout<<"詹挹辰好電"<<endl;
    cout<<"每一科都是電神\n";
    cout<<"明道希望Orz"<<"\n";
}
```

----


## 基本資料型態

### int  整數


---

### cin 輸入
```cpp=
#include<iostream>
using namespace std;
int main(){
    int a;
    int b=80;//直接初始化
    cin>>a;
    cout<<"我數學只有"<<a<<"分\n";
    cout<<"我月考國語只有"<<b<<"分\n";
}
```

----

### 方便的 cin 寫法

```cpp=
#include<iostream>
using namespace std;
int main(){
    int n,m,k;
    
    //可以這樣寫
    
    cin>>n;
    cin>>m;
    cin>>k;
    
    //也可以這樣寫
    
    cin>>n>>m>>k;
}
```

----


# 開始上新東西 !

---

### 程式語言只有 int , char , double
### 也太遜了吧...
### 其實還有更多的資料型態

----

### 整數部分


| 型態 | 範圍 |其他名稱|
| -------- | -------- | -------- |
| short     | -32,768 ~ 32,767     | __int16     |
| int | -2,147,483,648 ~ 2,147,483,647| signed ,  __int32
| long long|-9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807| __int64 |
還有 __int128 ~~(毒瘤)~~

----

### 如果看到前綴 unsigned 的話
### 代表他是非負整數、範圍會是 0 ~ 原本上界的兩倍大

---

### 浮點數(小數部分)

| 型態 | 範圍 |
| -------- | -------- |
| float     | 	3.4E +/- 38 (7 位數)  | 
| double |1.7E +/- 308 (15 位數)|
還有 __float128 ~~(毒瘤)~~

----

## 舉例

```cpp=
#include<iostream>
using namespace std;
int main(){
    double db;
    cin>>db;
    cout<<db;
}
```

----

## 特殊用法

```cpp=
#include<iostream>
#include<iomanip>
using namespace std;
int main(){
    // 如果只想輸出到小數第幾位
    double db;
    cin>>db;
    cout<<fixed<<setprecision(5)<<db;
}
```

---

### 其他

| 型態 | 範圍 |名稱|
| -------- | -------- |--------|
| bool     | 	false 或 true  | 布林值 |
| char | -128 ~ 127| 字元 |

----

### 等等 char 不是字元嗎 ? 儲存範圍是整數 ?

----

### ANS: char 在電腦時儲存為整數，但顯示出來會是字元
### 可以查表 !!!
http://kevin.hwai.edu.tw/~kevin/material/JAVA/Sample2016/ASCII.htm

---

## 舉例

```cpp=
#include<iostream>
using namespace std;
int main(){
    char a;
    cin>>a;
    cout<<a<<endl;
    cout<<int(a);
}
```

----

## 等等，int(a) 是什麼鬼?
## ANS:資料型態轉換

----

### 也就是說，藉由int(a)
### 我們將 char 以 int 的方式來呈現
### 當然也可以將 float 轉成 int , bool 轉成 int 等等

---

## 舉例

```cpp=
#include<iostream>
using namespace std;
int main(){
    bool a;
    cin>>a;//試著輸入任何數，看看結果
    cout<<a;
}
```

----

### 又發現了嗎？

----

### 對於bool, 
### 輸入 0 代表 0 (false)
### 輸入非0的數字 (1,-1,etc.) 都會是 1 (true) !

---

### 聽完覺得好複雜喔 ...
### 上MDCPP JUDGE 練習一次就會了 !!!
### 本日練習題~
http://mdcpp.mingdao.edu.tw/contest/9/problems
### 練習:1、11、12、13、14

----

# 運算子/式

----

## 奇怪，講師寫的程式只能將輸入的東西輸出
## ~~是不是有毛病阿~~

---

### 當然，平常的加減乘除都可以
### 但是 C++ 還有一些更酷的功能 !!!

----

## 1 賦值運算子

----

## 直接上程式碼
```cpp=
#include<iostream>
using namespace std;
int main(){
    int a=1;
    int b=3;
    cout<<a<<" "<<b<<endl;
    b=a;
    cout<<a<<" "<<b<<endl;
}
```

---

## 2 算術運算子

----

## 一定有的:
## +
## -
## *
## /

### ~~簡單國小數學~~

----

## 還有的:
## % (取餘數)

---

## 示範
```cpp=
#include<iostream>
using namespace std;
int main(){
    int a;
    int b;
    cin>>a;
    cin>>b;
    cout<<"a+b="<<a+b<<endl;
    cout<<"a-b="<<a-b<<endl;
    cout<<"a*b="<<a*b<<endl;
    cout<<"a/b="<<a/b<<endl;
    cout<<"a%b="<<a%b<<endl;
}
```

藉由這些運算子，我們就能讓使用者輸入一些數字，並且

----

## 這裡也有練習題喔 !!!
http://mdcpp.mingdao.edu.tw/contest/9/problems
## 練習:2、3、4、5、6

----

# 謝謝大家

