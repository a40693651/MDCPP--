---
title: 初探圖論
image: "https://i.pinimg.com/736x/26/e6/f4/26e6f4f90c298ad29818d390f32358f9.jpg"
slideOptions:
    theme: moon
---
## 圖論 I
作者：ernestii26

---

## Graph的表示



----

![](https://yuihuang.com/wp-content/uploads/2019/12/UILvyXHrwSmhoPMn.png)
圖是由邊和點所構成
有邊權和點權
題目比較常出現邊權
有向圖是邊具有方向不能逆行
無向圖是邊沒有方向兩邊都聯通(建兩個有向邊即可)

----

### 如何儲存一個圖
![](https://i.imgur.com/HJh9D1B.png)




----


### Adjacency Matrix
```cpp=
int G[mx][mx]; //mx=點的數量
void init()
{
    cin>>n>>m; //n是點的數量，m是邊的
    for(int i=0;i<m;i++)
    {
        cin>>a>>b>>c; //a,b之間有條邊 邊權為c
        G[a][b]=1; //如果有邊權就將1給成c
        G[b][a]=1; 
    }
}

```

----

## Adjacency List
無邊權
```cpp=
vector<int> G[mx];
void init()
{
    cin>>n>>m; //n是點的數量，m是邊的
    for(int i=0;i<m;i++)
    {
        cin>>a>>b; //a,b之間有條邊 
        G[a].push_back(b);
        G[b].push_back(a);
    }
}

```

----

有邊權
```cpp=
vector<pair<int,int> > G[mx];
void init()
{
    cin>>n>>m; //n是點的數量，m是邊的
    for(int i=0;i<m;i++)
    {
        cin>>a>>b>>c; //a,b之間有條邊 
        G[a].push_back({b,c});
        G[b].push_back({a,c});
    }
}

```

----

### 圖的遍歷(便利)


----

### DFS(深度優先搜尋)
Dfs是一種遞迴
![](https://upload.cc/i1/2022/05/01/gCAUSH.png)
需要一個vis陣列代表有沒有走過以面重複走

----

```cpp=
int vis[mx];
void dfs(int u)
{
    if(vis[u])
        return;
    vis[u]=1;
    for(int i=0;i<G[u].size();i++)
        dfs(G[u][i]);
}
```

----

### 小試身手
dfs時的時候除了vis陣列，有時也會需要建立別的陣列來紀錄狀況
[樹的高度與根(APCS201710)](http://mdcpp.mingdao.edu.tw/problem/B040)
這題有許多寫法其中一種是用之前學過的queue

---

### BFS(廣度優先搜尋)
比dfs難寫一點要用到queue
queue是先進先出



----

int vis[mx];
```cpp=
void bfs(int s)
{
    queue<int> q;
    q.push(s);vis[s]=1;
    while(q.size())
    {
        int tmp=q.front();q.pop();
        for (int i = 0; i < G[u].size(); i++)
        {
            int v = G[u][i];
            if (vis[v]) continue;
            q.push(v); vis[v] = 1;
        }
    }
}

```

----

![](https://miro.medium.com/max/1088/1*INwehwNaWrUmOvq_a5wMWg.gif)


----

## BFS的應用
當沒有邊權時，或邊權都是1時找最短路徑
[a982: 迷宮問題#1](https://zerojudge.tw/ShowProblem?problemid=a982)

---

### Dag
有向無環圖


----

## 無向圖
![](https://i.imgur.com/gYa1Jnd.png)


----

## 有向圖
![](https://i.imgur.com/Dgt8Qyi.png)




----

## 有向無環圖


----

![](https://i.imgur.com/w2rNmiw.png)



----

### Topological Sort!
![](https://i.imgur.com/ez8z3nr.jpg)




----

拓撲排序
一個頂點如果還沒被遍歷到，那從他連出去的邊(有向邊)所接的頂點就不能被遍歷到，


----

deg+queue
deg=degree(度數)
代表有幾條邊指向他

----

當一個頂點的deg是0
時，我們將他丟入queue裡面
這樣得出來的排序就是拓樸排序

----

```cpp=
while( q.size() )
    {
        tmp=q.front();
        q.pop();
        for(auto it: v[tmp])
        {
            deg[it]-=1;
            if(!de[it] )
            {
                q.push(it);
                ans.push_back(it);
            }
        }
    }
```

----

## 例題
[Course Schedule](https://cses.fi/problemset/task/1679)
[E - Unique Color](https://atcoder.jp/contests/abc198/tasks/abc198_e)
----

### 感謝收看