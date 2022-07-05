---
title: 圖論II
image: "https://i.pinimg.com/736x/26/e6/f4/26e6f4f90c298ad29818d390f32358f9.jpg"
slideOptions:
    theme: moon
---
## 圖論II
作者：ernest

---

## 如何判斷圖有沒有環

----

其中一個想法就是拓樸排序
拓樸排序只能用於無環圖

---

## Disjoint set
常用在圖論
有點偏資料結構
簡單好用

----

## 先來看看幾個例子
幫一些人分組
需要合併一些組
或查詢兩個人有沒有在同一組
有什麼方法

----

vector?  set?

----

幫每一組設立一個組長

----

![](https://i.imgur.com/im9L22s.jpg =900x)

----

![](https://i.imgur.com/lHPqCM4.png =900x)

----

### 初始化
一開始每個人都自己一組
所以要
for(int i=0;i<=n;i++)
    pa[i]=i;

----

### 如何找組長
遞迴(找上一個的組長)
```cpp=
int find(int x)
{
    if(par[x]==x)
        return x;
    return find(par[x]);
}
```

----

### 如何將不同組的人合併
將組長合併到同一組
```cpp=
void merge(int u,int v)
{
    int x=find(u);
    int y=find(v);
    par[x]=y;
}
```

----

### 遞迴太慢複雜度有可能到O(n)
優化技巧路徑壓縮
把自己的上一個直接改成組長
![](https://i.imgur.com/gcrR3Yv.png)

----

### 程式碼
```cpp=
int find(int x)
{
    if(par[x]==x)
        return x;
    return par[x]=find(par[x]);
}
```

----

## 練習
[d813: 10583 - Ubiquitous Religions](https://zerojudge.tw/ShowProblem?problemid=d813)
可以用bfs,dfs或disjoint set
[d831: 畢業旅行](https://zerojudge.tw/ShowProblem?problemid=d831)

---

### 最短路徑

----

邊權為一時可以用bfs
如果邊權不為一咧?

----

這裡會介紹3種演算法
分別是
dijkstra & bellman ford's & Floyd-Warshall

---

![](https://i.imgur.com/k6P4taQ.png =1000x)

----

## dijkstra
適用於無負邊的圖
O(n*n)
O(mlogn)

----

```cpp=
dis[ ] //起點到
vis[ ] //有沒有被遍歷過
vector<pair<int,int> > G[ ] //存圖
```

----

### 作法
先將起點設成0,其他設成無限大
從未vis的點挑最小的值並將其設為vis(因為沒有人能再更新他)，並更新他鄰近的點

----

```cpp=
void dijkstra(int s) //s起點
{
    memset(dis,0x3f3f3f3f,sizeof(dis));
    dis[s]=0;
    for(int i=0;i<n;i++)//做n次
    {
        int u=-1,minv=INF;//u代表未vis的點裡面最小的值
        //INF表無限大,minv是u的dis
        for(int j=0;j<n;j++)
        {
            if(!vis[j])
            {
                if(dis[j]<minv)
                    u=j,minv=dis[j];
            }
        }
        vis[u]=1;
        for(auto it:G[u])
        {
            int w=it.first,v=it.second;
            //w u到v的距離
            d[v]=min(d[v],d[u]+w);//更改鄰近的點
        }
    }
}

```

----

上面的複雜度是多少呢?

----

O(n*n)
因為鄰居不會超過n個

----

## dijkstra的優化
O(mlogn)

----

## 上面的程式可以優化哪裡呢?

----

明顯在找未vis的最小點時可以不用每個點都跑一次
我們可以用之前學過的priority_queue來找
這樣找的時間就會從O(n)就會變成O(logn)
把距離和點一起丟入priority_queue

----

## 丟入priority_queue裡距離的值可能會被更新
沒關係因未比較小的還是會先被拿出來

----

## 拿出去的時候才改
```cpp=
void dijkstra(int s)
{
    //pii=pair<int,int>
    memset(dis,0x3f3f3f3f,sizeof(dis));
    priority_queue<pii,vector<pii>,greater<pii> > pq;
//記得把pq改成小到大
    pq.push({0,s});
    while(pq.size())
    {
        int d=pq.top().first,u=pq.top().second
        if(dis[u]!=INF) //把還沒改過的留下來
            continue;
        dis[u]=d;
        for(auto it:G[u])
        {
            pq.push({d+it.first,it.second});
        }
    }
}
```

----

## 隨時改的版本
```cpp=
void dijkstra(int s)
{
    //pii=pair<int,int>
    memset(dis,0x3f3f3f3f,sizeof(dis));
    priority_queue<pii,vector<pii>,greater<pii> > pq;
//記得把pq改成小到大
    pq.push({0,s});
    dis[s]=0;//跟前面不同要先改
    while(pq.size())
    {
        int d=pq.top().first,u=pq.top().second
        if(d!=dis[u]) //被改過了，所以不採用
            continue;
        for(auto it:G[u])
        {
            int a=it.first,b=it.second;
            if(d+a<dis[b])
            {
                dis[b]=d+a;//馬上改
                pq.push({d+a,b});
            }
        }
    }
}
```

----

## 例題
[Shortest Routes I](https://cses.fi/problemset/task/1671/)

---

### Bellman Ford's
適用於負邊可找負環

----

dijkstra不能用於負邊是因為
dis存的是起點到任一點的距離
如果有一條邊連的不是起點
那後來再更新的時候這條邊會使已經
vis的點再次被更新導致錯誤

----

### 存邊
edge list
{u,v,w};
u到v的距離為w
```cpp=
struct Edge
{
    int u,v,w;
};
```

----

## 作法
走n-1次每次都把m個邊跑過一次
可以更新的話就更新

----

```cpp=
vector<Edge> edges[m];
void BellmanFord(int s)
{
    memset(dis,0x3f3f3f3f,sizeof(dis));
    dis[s]=0;
    for(int i=0;i<n-1;i++)
        for(int j=0;j<m;j++)
        {
            Edge e=edges[j];
            dis[e.v]=min(dis[e.v],dis[e.u]+e.w);
        }
           
}
```

----

## 為什麼是跑n-1次
想一下什麼時候是最糟其況
那就是排成一條鍊那要更新到最遠的點就需要n-1次
其實跑n次也可以
多跑一次耶(ya沒差

----

## SPFA
bellman ford的優化
為什麼bellman ford比較慢
因為他每個邊都跑
優化的方法就是被更新過的點才去更新他周圍的點

----

## 作法:
改成鄰接表(adjacency list)來存圖
一開始將起點加入queue
每次從queue裡取出一點
更新他的周圍
如果更新成功
將更新成功的點加入queue

----

```cpp=
//G[u].push_back({v,w});
void spfa(int s)
{
    memset(dis,0x3f3f3f3f,sizeof(dis));
    dis[s]=0;
    inq[s]=1;//已經在queue裡面了
    queue<int> q;
    q.push(s);
    while(q.size())
    {
        int tmp=q.front();q.pop();
        inq[tmp]=0;
        for(auto it:G[tmp])
        {
           if(dis[it.first]>dis[tmp]+it.second)
           {
               dis[it.first]=dis[tmp]+it.second;
               if(!inq[it.first])
                   q.push(it.first);
               inq[it.first]=1;
           }
        }
    }
}

```

----

SPFA的複雜度大約是O(kE),k是每個點的平均進隊次數(一般的，k是一個常數，在稀疏圖中小於2)
SPFA最差情況有可能和bellman ford一樣慢
所以在沒有負邊的情況下dijkstra的時間還是優於spfa

----

## 除了最短路的應用
bellman ford還可以用在找負環
有負環就沒最短路
因為一直跑就一直變小
所以當bellman ford 跑到第n次還再更新
那就是有負環

----

## 負環
![](https://i.imgur.com/MUUeSgW.png =400x)


----

## 例題
[Cycle Finding](https://cses.fi/problemset/task/1197)

---

## Floyd-Warshall
適用於負邊
O(n^3)

----

最簡單的(?
可以找出任兩點的最短距離

----

## 作法
使用adjacency matrix儲存
dis[i][j] i到j的距離

----

```cpp=
void FloydWarshall()
{
    for(int k=0;k<n;k++)
        for(int i=0;i<n;i++)
            for(int j=0;j<n;j++)
                dis[i][j]=min(dis[i][j],dis[i][k]+dis[k][j]);
}

```

----

暴力的時候蠻好用的

----

## 例題
[d536: 3. 圖形迴圈偵錯問題](https://zerojudge.tw/ShowProblem?problemid=d536)

---

## 謝謝大家
程式碼皆屬虛擬code(編譯不會過):
可能不小心少;之類的
如果有其他程式錯誤恭請指教(應該不會 by jameslee)
![](https://i.imgur.com/1Nfco7D.jpg)

---

![](https://i.imgur.com/oSJbjD3.jpg)

----

字有點多並不是一個好的ppt(我才不管咧)