###### tags: `MDCPP`

# APCS安裝教學

----

APCS測試環境安裝教學

----

為甚麼要裝APCS的測試環境

----

因為APCS使用了不同於windows的**作業系統**

*看不懂作業系統是甚麼很正常，後面有時間我會科普一下

----

用了不同的作業系統就要先熟悉嗎?使用起來會差很多嗎?

----

欸對，會差很多

我們之前就碰過有人不會用APCS的作業系統

結果花了1個小時才能開始寫程式

浪費掉一堆檢定時間，成績想當然也沒很好

----

先到他的[官網](https://apcs.csie.ntnu.edu.tw/index.php/info/environment/)
![](https://i.imgur.com/GUIflvA.png)

這是關於她環境的設定
看不懂很正常，沒關係

----

往下滑到

![](https://i.imgur.com/Q69jnQR.png)

這個地方

----

先點Virtual box

到這個官網

![](https://i.imgur.com/4pyYKMe.png)

----

先來簡介甚麼是Virtual box

----

他是一個可以讓你裝虛擬環境的東西

可以想像成在你的電腦上裝另一台電腦

----

我們使用這個的Virtual算是最好入門的虛擬環境軟體

----

然後我們點這個下載

![](https://i.imgur.com/shGkFNz.png)


----

會得到這個檔案

![](https://i.imgur.com/g1f7U9r.png)

點開他

----

![](https://i.imgur.com/uii9vv0.png)

出現這個

----

然後就是大家安裝軟體最喜歡的

狂按Next大法了

反正管他甚麼的，甚麼都看不懂，連點Next他就裝好了

![](https://i.imgur.com/G05a45Q.png =500x)

----

沒啦，總之中間是調設定用的

這次還不需要改

----

![](https://i.imgur.com/sdShNYu.png =600x)
裝好之後打開長這樣

上面那個不要理他，那是我私底下用的環境

----

有了Virtual box之後

我們就要把需要的檔案餵給他了

----

回到APCS[官網](https://apcs.csie.ntnu.edu.tw/index.php/info/environment/)
![](https://i.imgur.com/J1dxPmw.png)

----

這次換點這個
![](https://i.imgur.com/brXw2TI.png)

----

![](https://i.imgur.com/CL9DuWw.png)

點仍要下載

反正他怎麼警告你們也不會管的
都嘛直接下載嘛，尤其那幾個感覺就載過很多奇怪東西的

----

![](https://i.imgur.com/N0XATG5.png)
會得到這個檔案
有點大

----

接著打開我們的Virtual box

點Tool -> New

![](https://i.imgur.com/mv5w2FG.png)

創建一個新環境

----

type選linux
Version選Ubuntu 64bit
![](https://i.imgur.com/aWO1K0B.png)

----

很好，現在又出現新名詞了
linux跟Ubunutu64又是尛(ㄇㄚˊ)

----

再來簡介一下

----

linux是我們提到的作業系統的一種

~~不是林姓商人發明的~~
![](https://i.imgur.com/WCLHCxC.png)

有機會後面再提

----

Ubuntu 64bit中

Ubuntu是linux的版本

至於為甚麼選Ubuntu，是因為他是最為盛行的**桌面版linux**

----

一般linux
![](https://i.imgur.com/9vLUlBu.png =400x)
Ubunutu
![](https://i.imgur.com/NokhUQp.png =400x)


----

回到這裡
![](https://i.imgur.com/13YVafv.png)

----

按Next之後出現這個畫面
![](https://i.imgur.com/pgpvv4J.png)
他會要你選擇要分配的**記憶體**容量

APCS用的是4096MB，所以就選4096

----

Next之後是這個
![](https://i.imgur.com/oNDPVLx.png)
這是設置**硬碟**的選項
我們選第一個，中文應該是不加入虛擬硬碟

----

![](https://i.imgur.com/YNeYJGz.png)
他會跳出一個警告

意思大概是:
如果你不加入虛擬硬碟，你就不能夠下載作業系統
同時，你只能使用虛擬光碟或透過網路啟動他

----

好了之後回到畫面，按Add旁邊的Setting
![](https://i.imgur.com/VHhzkyK.png)

----

選第四個storage，中文是儲存空間，也就是我們剛剛沒有用的硬碟
![](https://i.imgur.com/4hIq16d.png)

----
![](https://i.imgur.com/JUhvJH1.png)

中間可以看到這個，理論上兩個都是空的
因為我們沒有塞硬碟進去

----

![](https://i.imgur.com/JUhvJH1.png)

這張圖上可以看見兩個東西
一個是IDE，一個是SATA
他們分別代表不同的控制器
總之我們要選IDE那個用

----

兩者差別大概是
SATA更高效
但APCS用的IDE是可以在更多樣的電腦上使用的版本

----

按這個
![](https://i.imgur.com/JBBK2np.png)
加入光碟

----

選Add
![](https://i.imgur.com/Od5NeFl.png)

----

把我們從APCS官網下載下來的ISO檔丟上去
![](https://i.imgur.com/wthVaAg.png)

tips:ISO檔全名光碟映像檔，所以我們剛剛才選光碟圖案

----

最後點choose
恭喜你設定完了
![](https://i.imgur.com/RAauN7j.png)
阿記得按OK嘿

----

回到這裡按start啟動他吧
![](https://i.imgur.com/q7GijY5.png)

----

打開變這樣
![](https://i.imgur.com/TehoXlX.png)

點一下螢幕就可以進去操控
如果要從螢幕跳出來，按一下右邊的Ctrl就好

----

接著建議先開一個資料夾存程式碼
右鍵create folder，名字隨便取
![](https://i.imgur.com/NVz4jBr.png)

----

接著開我們的codeblock
他就是一個IDE，跟DevC++是一樣的意思
![](https://i.imgur.com/bjOIfzu.png)


----

選file，注意選下面那個，上面那個是虛擬機的file
![](https://i.imgur.com/1wACBNc.png)

----

New file
![](https://i.imgur.com/a6jwnsA.png)

----

選C++ source
![](https://i.imgur.com/19KS8Dq.png)

----

Next到這個畫面
![](https://i.imgur.com/S5BxX3g.png)
點``...``

----

進這個畫面選Desktop(桌面)
![](https://i.imgur.com/Ren5bIB.png)

----

找到我們創建的資料夾，點進去
![](https://i.imgur.com/08rbPax.png)

----

幫你的文件取名字，記得結尾要加CPP，不然不會動
![](https://i.imgur.com/j0OFnvv.png)
最後按右下save -> finish 就好了

----

可以開始打程式了
![](https://i.imgur.com/2pTjto8.png)

----

上面這3個分別是: 編譯、執行、編譯並執行，打好按他們就可以動了
![](https://i.imgur.com/JcpiF1j.png)

----

教學結束，感謝各位
![](https://i.imgur.com/vlcvYoQ.jpg =800x)
