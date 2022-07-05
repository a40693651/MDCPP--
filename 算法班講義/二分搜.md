# 11 / 1 MDCPP 二分搜

---

## 上次題目講解 

---

[ T009 動態中位數 ](http://mdcpp.mingdao.edu.tw/contest/19/problem/T009)
這題是我認為比較難的一題，需要動動腦筋思考 ~
在上次上課的時候，我發現有許多人想要將 $std::set$ 裡面的東西取中位數，很可惜的是不行的喔 ~

---

有個小題示想告訴你們，就是說寫題目除了要想好要利用什麼資料結構之外，更要了解到要針對題目所給的**中位數**，利用他的一些性質進行操作

---

有些人可能會想要每次加入數字完後都進行排序，很可惜的，這樣會導致時間複雜度太高而得到一個 $TLE$ 

---

由於 $std::sort$ 的複雜度是 $O(nlogn)$，所以排序 $N$ 遍會導致複雜度是 $O(n^2logn)=1E11$，這樣的複雜度顯然不是好的。

---

我們會發現，題目要求我們每兩次輸出一次答案，那我們可以透過觀察，發現中位數是如何改變的

---

我們會發現，若接下來的兩個數 都小於 或 都大於 目前中位數的話，中位數就會改變，而且新的中位數一定會是比原本中位數中 小的最大值 或 大的最小值

---

那我們現在的問題是，如何得到 原本中位數中 小的最大值 或 大的最小值 ? 因為本題強調 **動態** ，代表我們要用動態的資料結構維護他，那當然就是 $std::set$拉 ~

---

我就不多做解釋了，看完影片跟code就會了喔 ~

```cpp=
// Of course you won't get AC if you submit this code without debugging
#include <iostream>
#include <set>
using namespace std;

int main()
{
    set<int> a;
    int n, x, y, k;
    cin >> n >> x;
    a.insert(x);
    set<int>::iterator it = a.begin();
    for (int i = 0; i < n / 2; i++)
    {
        cout << *it << " ";
        cin >> x >> y;
        a.insert(x);
        a.insert(y);
        k = 0;
        if (x >= *it) k++;
        if (y >= *it) k++;
        if (k == 2) it++;
        else if (k == 0) it--;
    }
}
```

---

## 影片解釋
![](https://i.imgur.com/EcxUfgQ.gif)

---

[ T010 先到先服務 ](http://mdcpp.mingdao.edu.tw/contest/19/problem/T010)

---

這題較上一題簡單許多
我們可以發現，我們讓先到的前 $M$ 位客人進入櫃檯，那我們每到有人結束的時候，就將當前最先到的人接下去。
我們要如何確認有人結束 ? 那不就是要取時間最小的人嗎 ?
那我們就可以利用 $std::set$ 將最小結束時間的人取出，再將新的人的時間加上他，並且放入 $std::set$。

---

```cpp=
#include <iostream>
#include <queue>
using namespace std;
int arr[200000];
int main()
{
    ios::sync_with_stdio(0);
    cin.tie(0);
    long long n, m, x, ans;
    cin >> n >> m;
    priority_queue<int, vector<int>, greater<int>> q(arr, arr + m);
    for (int i = 0; i < n; i++)
    {
        cin >> x;
        //int time=q.top();
        //int c=q.top()+x;
        //q.pop();
        //q.push(q.top()+x);
        q.push(q.top() + x);
        q.pop();
    }
    while (!q.empty())
    {
        ans = q.top();
        q.pop();
    }
    cout << ans;
    return 0;
}
```

```cpp=
#include <iostream>
#include <queue>
using namespace std;
int arr[200000];
int main()
{
    ios::sync_with_stdio(0);
    cin.tie(0);
    long long n, m, x, ans;
    cin >> n >> m;
    multiset<int> st;
    while(m--) st.insert(0);
    for (int i = 0; i < n; i++)
    {
        cin >> x;
        st.insert(*st.begin() + x);
        st.erase(st.begin());
    }
    while (!st.empty())
    {
        ans = *st.begin();
        st.erase(st.begin());
    }
    cout << ans;
    return 0;
}
```
---

## 進入正題 -- 二分搜

---

二分搜是什麼哩 ? 他是一種讓我們快速在資料結構中查找我們所要資料的方法。
大家應該都學過**循序搜尋法**了，但我不講那是什麼你應該以為你不會。

---

### Example of 循序搜尋法

```
給你一個陣列及一個數字 K，問你陣列中等於 K 的數字有幾個
```

---

簡單啦！這不就直接遍歷陣列就好了 ?
對。。。

---

## 我們再來看一個經典問題 -- 摩斯密碼

```
給你一個範圍 [1~k]，並且有一個摩斯密碼，問你最多要猜幾次才能猜到答案
```

---

這個問題大家都會吧 ~
直接從 [1~k] 的詢問的複雜度是 $O(k)$，非常不可取的複雜度
我們當然都知道我們可以透過每次從中間開始猜，若比較大，就往 [中間數~右界數]猜，反之則然。
則如此一來的複雜度是$O(logk)$，是一個非常快的算法。

---

其實這就是二分搜的精髓，若序列中的值有單調性，我們每次就能從中間開始找，確認解答的位置再繼續找，直到找到為止。

---

### 等等，單調性是什麼拉 ... 

---

所謂的單調性是指，序列中的值跟答案的關係會遞增或遞減，像是摩斯密碼，若把序列、答案、每次詢問的回答列出來，他會長下面這樣子

密碼 = 5 ， 範圍 [1~7]

| 數字 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
| ------- | -------- | -------- | -------- | ------- | ------- | ------- | ------- | 
| 與答案距離 | -4 | -3 | -2 | -1 | 0 | 1 | 2 |

註：若與答案距離為負，代表答案在左邊，反之則然
發現了嗎 ? 

---

## 例題 -- 經典題，最接近小於等於 K 的數字

```
給你 一個陣列 及 Q 次詢問 K，問你最接近小於等於 K 的數字是誰
陣列大小 <= 1E5 ， Q <= 1E5 ， K <= 1E9 ， Time Limit = 1.00 second
```

---

我們發現，在一次詢問的時候，我們可以直接遍歷陣列得到答案，複雜度  $O(N)$，但是會發現這次有 $Q$ 次詢問，這樣的複雜度會是 $O(NQ)$，明顯超出了 C++ 一秒跑 1E9 次的量值。

---

那我們來想想如何利用二分搜。
我們上面有提到，二分搜最重要的就是單調性，我們才能省略許多部份的查詢。

---

我們會發現陣列的順序沒有差別，那我們嘗試將陣列 **排序** 一遍
我們會發現，ㄟ，排序是不是會造成單調性阿 ?
如果你想到這裡，就快接近答案了 !

---

我們可以嘗試利用二分搜的模型。我們先對陣列排序後，我們取中間數，確認他是否大於 K ，若是的話，我們可以直接將範圍縮小為 [ 左界 ~ 中間 ]，反之，我們得到了一個小於等於 K 的數，我們先將他記下來，接著只要重複上面的步驟就行了 ~

---
### CODE
```cpp=
#include <iostream>
using namespace std;
const int maxn = 1e5 + 50 ;
int main() {
    int n,q;
    cin>>n>>q;
    int arr[maxn];
    for(int i=1;i<=n;i++) {
        cin>>arr[n];
    }
    sort(arr+1,arr+1+n);
    while(q--) {
        int l=1,r=n,ans=-1,k;
        cin>>k;
        while(l<=r) {
            int mid=(l+r)/2;
            if(arr[mid]>k) {
                r=mid-1;
            } 
            else {
                ans=mid;
                l=mid+1;
            }
        }
        if(ans!=-1) cout<<ans<<endl;
        else cout<<"Not found\n";
    }
}
```

---

讓我們一步一步闡析這個 code 
首先，$l$、$r$ 代表的是當前區間的左右界
**Line 13 :** 取出中間數
**Line 14~16 :** 確認是否大於 $K$
**Line 17~20 :** 反之記錄答案

---

```That's it ! You have just learned new algorithm -- binary search !```


---

### 另一種二分搜寫法

---

```cpp=
// Another type of binary search
// Jump Search

#include <iostream>
using namespace std;
const int maxn = 1e5 + 50 ;
int main() {
    int n,q;
    cin>>n>>q;
    int arr[maxn];
    for(int i=1;i<=n;i++) {
        cin>>arr[n];
    }
    while(q--) {
        int ans=-1,pos=1,k;
        cin>>k;
        for(int i=n;i>0;i=i/2) {
            if(arr[pos+i]<=k) {
                ans=pos+i;
                pos+=i;
            }
            else if(arr[pos]<=k) {
                ans=pos;
            }
        }
        if(ans!=-1) cout<<arr[ans]<<endl;
        else cout<<"Not found\n";
    }
}
```
---

這種二分搜寫法有點難懂，我們也來看一下
他是利用二分搜的 **中間數** 每次移動位置會除以二的特性來寫的
**Line 15~19 :** 確認是否小於等於 $K$ ， 有的話記錄答案
**Line 20~22 :** 確認不加的話是否小於等於 $K$

---

偷偷告訴你們，上面那題有 STL 函式可用...

---

### STL 內建函式
```
lower_bound (ForwardIterator first, ForwardIterator last,const T& val);
// 代表在這個範圍內最小、大於等於 val 的數的 指標 / 迭代器
upper_bound (ForwardIterator first, ForwardIterator last,const T& val);
// 代表在這個範圍內最小、大於 val 的數的 指標 / 迭代器
```

---

大家有可能會發現，這不是跟我們題目要的剛好相反嗎 ? 那有什麼用 :cry: 
其實，我們可以利用 指標 / 迭代器 可以 ++/-- 的特性，我們將 upper_bound 所得到的 指標 / 迭代器 -- 就是我們要的功能 ~

---

### 範例 CODE ( BY STL )
```cpp=
// auto it1
// auto it2
// int num = it2-it1 ;
#include <iostream>
using namespace std;
const int maxn = 1e5 + 50 ;
int main() {
    int n,q;
    cin>>n>>q;
    int arr[maxn];
    for(int i=1;i<=n;i++) {
        cin>>arr[n];
    }
    sort(arr+1,arr+1+n);
    while(q--) {
        int ans=-1,k;
        cin>>k;
        auto it=upper_bound(arr+1,arr+1+n,k);
        if(it==arr+1+n) cout<<"Not found\n";
        else cout<<*(--it)<<endl;
    }
}
```

是不是簡潔很多呢 ~ 不過，我們等下會看到並不是所有的二分搜都能利用到 STL。

---

## std::set 的 upper_bound, lower_bound

---

上禮拜教的 std::set 又來拉 ~
std::set有著與上面的陣列相同的二分搜功能，複雜度同樣也是 $O(logn)$
所以我們能藉由std::set動態的特性，完成更多題目 !
他的語法如下

```
// st 是一個 set
st.upper_bound(x)
st.lower_bound(x)
```

---

## 例題 - 經典題，動態最接近小於等於 K 的數字

---

```
給你 Q 次詢問，每次詢問會有兩種：
1.問你最接近小於等於 K 的數字是誰
2.新增一個數 K
陣列大小 <= 1E5 ， Q <= 2E5 ， K <= 1E9 ， Time Limit = 1.00 second
```

---

這次我們又更進化了 !
一般的二分搜無法進行動態增加值的動作，但利用 std::set 就沒問題 !

---

```cpp=
#include <iostream>
using namespace std;
const int maxn = 1e5 + 50 ;
int main() {
    int q;
    cin>>q;
    multiset<int>st;
    while(q--) {
        int ans=-1,t,k;
        cin>>t;
        if(t==1) {
            cin>>k;
            auto it=st.upper_bound(k);
            if(it==st.end()) cout<<"Not found\n";
            else cout<<*--it<<endl;
        }
        else {
            cin>>k;
            st.insert(k);
        }
    }
}
```

---

## 對答案二分搜 ( 外掛二分搜 )

---

這是一個很常見的二分搜類型，變化更大。
前面我們講的二分搜都是在一個資料結構上進行的，但這次我們要對答案二分搜 !
我們有時候遇到一種類型的問題是 : 給你一些條件，問你最少 / 最多要多少才能滿足條件

---

我知道這很玄，所以我們直接來看例題ㄅ ~

---

[ 上一屆的模擬賽題 ](http://mdcpp.mingdao.edu.tw/problem/T064)

```
題目解釋：
有一個陣列 及 一個數字 M，你可以用 M 次覆蓋格子
覆蓋的方法是指：每次覆蓋會有總和，要將全部的都覆蓋一起
問你所有覆蓋次數中，一次覆蓋最多量的那次為 K 次，問你 K 最小是多少
N, M <= 2E6, Ni <= 1e4
```

---

直接看的話可能會想要利用數學解 ? 說不定有，但我數學不太好
我們在這種情況下，就出現了上面 `給你一些條件，問你最少 / 最多要多少才能滿足條件` 的模型，並且我們不知道要怎麼直接算出答案，那我們就利用外掛二分搜吧 ~

---

外掛二分搜要怎麼執行呢 ? 我們發現答案一定位於 [1~N] 的範圍，那我們要求最小值，可以用二分搜也是因為 **數字越大越有機會達成這個條件**。

---

現在我們的問題轉換成，我們已經知道最大值能是多少，那我們要如何確認是否能被達到的。
很簡單，我們就直接每次直接掃過去陣列，直接一直加上去，若能加就加，不能加就換一個新的，最後看沒有超過 M 次就行了 ~

---

### code

---

```cpp=
// Same, you won't get AC without debugging
#include <iostream>
using namespace std;
const int maxn = 2e5 + 5 ;
int d[maxn],n,k;
bool check(int num)
{
    int sum=0,cc=1;
    for(int i=1;i<=n;i++)
    {
        if(d[i]+sum<=num) sum+=d[i];
        else if(d[i]>num) return false;
        else cc++,sum=d[i];
    }
    if(cc<=k) return true;
    else return false;
}
int solve(int l,int r)
{
    int best=-1;
    while(l<r)
    {
        int mid=(l+r)>>1;
        bool c=check(mid);
        if(c) best=mid,r=mid-1;
        else l=mid+1;
    }
    return best;
}
signed main()
{
	cin>>n>>k;
	for(int i=1;i<=n;i++) cin>>d[i];
	cout<<solve(0,1e9*n-1);
}
```

---

## THANKS FOR LISTENING

---

![](https://i.imgur.com/EfFMgOa.jpg)

