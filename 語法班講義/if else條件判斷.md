---
title: if else條件判斷
image: "https://besthqwallpapers.com/Uploads/27-1-2019/78554/thumb2-megumin-artwork-protagonist-konosuba-series-manga.jpg"
slideOptions:
    theme: moon
---
###### tags: `MDCPP講義`
# if else 條件判斷

by explosionnn

---


### 讓我們先來複習一下之前的東西...

----

### cin (輸入) 跟 cout (輸出)
```cpp=
#include<iostream>
using namespace std;
int main(){
    int a;
    cin >> a;
    cout << a << "\n";
}
```

----

### 變數型態

int -> 整數 (1、0、-1、420、32768)
char -> 字元 (a、b、1、@、#、$、?)
float -> 浮點數 (1.0、2.6、3.14159)
double -> 浮點數 (1.0、2.6、3.14159)
bool -> 布林值 (true、false、1、0)

```cpp=
#include<iostream>
using namespace std;
int main(){
    int a;
    char c;
    float f;
    double db;
    bool b;
}
```

----

### 運算子/式

----

#### 賦值運算子

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

----

#### 算術運算子

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

---

### 開始進入新主題 
### if / else

----

### 什麼是 if / else

![](https://i.imgur.com/mnW96A8.png)
![](https://i.imgur.com/jgvCW5a.png)

----

### 在講解語法之前...

----

#### 情境一
小宇來到一個商店，商店有賣一瓶25元的可樂，如果小宇帶的錢足夠就買一瓶可樂。

----

#### 情境二
小宇來到一個商店，商店有賣一瓶25元的可樂，如果小宇帶的錢足夠就買一瓶可樂，否則離開商店。

----

#### 情境三
小宇來到一個商店，商店有賣一瓶25元的可樂，也有賣一瓶10元的礦泉水，如果小宇帶的錢足夠買一瓶可樂就買一瓶可樂，否則的話如果小宇帶的錢只足夠買一瓶礦泉水就買一瓶礦泉水，否則就離開商店。

----

### 語法

----

#### if

```cpp=
#include<iostream>
using namespace std;
int main(){
    if( /*判斷條件*/ ){
        //符合條件，執行大括號的程式碼
    }
}
```

----

#### if / else

```cpp=
#include<iostream>
using namespace std;
int main(){
    if( /*判斷條件*/ ){
        //符合條件，執行這個大括號的程式碼
    }else{
        //不符合條件，執行這個大括號的程式碼
    }
}
```

----

#### if / else if / else

```cpp=
#include<iostream>
using namespace std;
int main(){
    if( /*判斷條件1*/ ){
        //符合條件1，執行這個大括號的程式碼
    }else if( /*判斷條件2*/ ){
        //不符合條件1，但符合條件2，執行這個大括號的程式碼
    }else{
        //不符合條件1，也不符合條件2，執行這個大括號的程式碼
    }
}
```

---

### 判斷條件要放什麼呢？

----

#### 比較運算子

等於 ==
不等於 !=
大於 >
大於等於 >=
小於 <
小於等於 <=

----

#### 程式碼

```cpp=
#include<iostream>
using namespace std;
int main(){
    int a = 10;
    double b = 20;
    char c = 'f';
    bool d = true;
    
    if(a == 10){
        cout << "a等於10" << endl;
    }
    
    if(b < 30.0){
        cout << "b小於30" << endl;
    }
    
    if(c == 'f'){
        cout << "c等於f" << endl;
    }
    
    if(d == true){
        cout << "d等於true" << endl;
    }
}
```

----

#### 省略比較運算子

```cpp=
#include<iostream>
using namespace std;
int main(){
    int a = 1;
    bool b = false;
    
    if(a){
        cout << "123" << endl;
        //輸出123
    }
    
    if(b){
        cout << "456" << endl;
        //不輸出456
    }
}
```

----

#### 邏輯運算子
和 && and
或 || or
否定 !

----

#### 程式碼

```cpp=
#include<iostream>
using namespace std;
int main(){
    int a = 10, b = 20;
    int c = 50, d = 75;
    int e = 100;
    if(a == 10 && b == 20){
        cout << "hey you" << endl;
    }
    
    if(c > 40 || d < 70){
        cout << "yeah you" << endl;
    }
    
    if(!(e == 50)){
        cout << "we have a gift for you" << endl;
    }
}
```

----

#### 搭配加減乘除

```cpp=
#include<iostream>
using namespace std;
int main(){
    int a = 10, b = 15;
    if(a + b == 25){
        cout << "巨槌瑞斯" << endl;
    }
}
```

---

### 重要補充

----

#### 情境四
小宇來到一個商店，商店有賣一瓶25元的可樂，也有賣一瓶10元的礦泉水，如果小宇帶的錢足夠買一瓶可樂就買一瓶可樂，如果小宇剩下的錢足夠買一瓶礦泉水就買一瓶礦泉水。

----

#### 兩個 if

```cpp=
#include<iostream>
using namespace std;
int main(){
    if( /*判斷條件1*/ ){
        //符合條件1，執行這個大括號的程式碼
    }
    
    if( /*判斷條件2*/ ){
        //符合條件2，執行這個大括號的程式碼
    }
}
```

----

#### 巢狀if

```cpp=
#include<iostream>
using namespace std;
int main(){
    if(){
        if(){
            if(){
                ...
            }
        }
    }
}
```

---

### 題目

MDjudge a00000 奇奇偶偶奇奇偶：
http://mdcpp.mingdao.edu.tw/problem/a00000

MDjudge A014 閏年判斷：
http://mdcpp.mingdao.edu.tw/problem/A014

MDjudge A015 我能結婚嗎?：
http://mdcpp.mingdao.edu.tw/problem/A015
