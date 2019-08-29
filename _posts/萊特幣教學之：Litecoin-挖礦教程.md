---
title: 萊特幣教學之：Litecoin 挖礦教程
date: 2014-08-29 20:18:47
tags: [blogger, litecoin]
categories: Blogger
---

除了比特幣之外，價格最堅挺的就要數萊特幣了。Mt.Gox也宣佈最近有支持萊特幣的計劃。比起比特幣的專業礦機，萊特幣挖礦比較平民化，用普通的電腦就可以。編者今天就來講一下萊特幣的挖礦方法。

<!-- more --> 

Litecoin Mining
第一步 下載萊特幣客戶端
萊特幣客戶端可以點擊這裡下載，讀者可以找到適合自己操作系統的版本。
安裝過程非常簡單，只要等待數據塊下載完畢就可以使用了。
Go to top
第二步 下載挖礦軟件
對於CPU挖礦 

首先你需要下載pooler-cpuminer來進行CPU挖礦。下面的列表中有各個操作系統的版本下載。選擇適合你的版本，下載並解壓縮。


Windows 32 bits Version 2.23
Windows 64 bitsVersion 2.22
Linux 32 bits Version 2.2.3
Linux 64 bits Version 2.2.3
Macintosh 32 bits Version 2.1.2
Macintosh 64 bits Version 2.2.2

對於網絡狀況不好的童鞋，可能還需要安裝Stratum mining proxy。將下載好的mining_proxy放到pooler-cpuminer的壓縮後的文件夾中：

Go to top
第三步 註冊一個礦池賬號。下面是一些著名的萊特幣礦池，選擇一個你喜歡的，註冊一個賬號。

◼	WeMineLTC	5,543.7 MH/s
◼	Coinotron	4,406.2 MH/s
◼	give-me-ltc.com	4,379.9 MH/s
◼	litecoinpool.org	3,247.8 MH/s
◼	Pool-X.eu	768.2 MH/s
◼	P2Pool	758.5 MH/s
◼	Hypernova	698.0 MH/s
◼	Netcode Pool	396.5 MH/s
◼	LiteBonk	236.4 MH/s
◼	CoinHuntr	216.1 MH/s
◼	burnside’s Pool	209.2 MH/s
◼	Litepool.eu	164.1 MH/s
◼	Elitist Jerks	160.6 MH/s
◼	litepool.ru	139.3 MH/s
◼	Nushor’s Pool	118.3 MH/s


以coinotron為例。在註冊完成後，自定義一個礦工號和密碼，並選擇LTC。
例如：name：vonyaven.1  password：1  ，參考下圖。

然後在windows的CMD中運行miningproxy,並保持運行狀態。 coinotron萊特幣的Stratum端口是3334，所以在-p（port）參數後面寫上3334。紅色字體為運行的CMD命令。
E:\pooler-cpuminer-2.2.2-win64\miningproxy -pa scrypt -o coinotron.com -p 3334
2013-07-17 10:43:01,042 WARNING proxy jobs. # C extension for midstate n
ot available. Using default implementation instead.
2013-07-17 10:43:01,651 INFO proxy miningproxy.main # Stratum proxy version: 1.
3.0
2013-07-17 10:43:01,654 INFO proxy miningproxy.main # Trying to connect to Stra
tum pool at coinotron.com:3334
2013-07-17 10:43:01,657 INFO proxy miningproxy.main # Setting PoW algo: scrypt
2013-07-17 10:43:05,066 INFO stats stats.printstats # 1 peers connected, state
changed 1 times
2013-07-17 10:43:05,068 INFO proxy miningproxy.onconnect # Connected to Stratu
m pool at coinotron.com:3334
2013-07-17 10:43:05,069 INFO proxy miningproxy.onconnect # Subscribing for min
ing jobs
2013-07-17 10:43:05,480 INFO proxy miningproxy.main # ————————-
———————————————-
2013-07-17 10:43:05,480 INFO proxy miningproxy.main # PROXY IS LISTENING ON ALL
IPs ON PORT 3333 (stratum) AND 8332 (getwork)
2013-07-17 10:43:05,480 INFO proxy mining_proxy.main # ————————-
———————————————- 
Go to top
第四步 運行pooler-cpuminer ，打開CMD運行下面的命令或者將下面內容寫入後綴名為bat的文件運行。
E:\pooler-cpuminer-2.2.2-win64\minerd -a scrypt -r 1 -t 4 -s 6 -o http://127.0.0.1:8332 -O vonyaven.1:1
注意，命令格式為：minerd -a scrypt -r 1 -t 4 -s 6 -o http://127.0.0.1:8332 -O 你定義的礦工名字：礦工密碼

C:\Users\my-pc\Desktop>E:\pooler-cpuminer-2.2.2-win64\minerd -a scrypt -r 1 -t 4
-s 6 -o http://127.0.0.1:8332 -O vonyaven.1:1
[2013-07-17 10:50:59] 4 miner threads started, using 『scrypt』 algorithm.
[2013-07-17 10:50:59] Long-polling activated for http://127.0.0.1:8332/lp
[2013-07-17 10:51:00] thread 1: 4104 hashes, 4.08 khash/s
[2013-07-17 10:51:00] thread 0: 4104 hashes, 4.02 khash/s
[2013-07-17 10:51:00] thread 3: 4104 hashes, 3.89 khash/s
[2013-07-17 10:51:00] thread 2: 4104 hashes, 3.70 khash/s 

這樣，一個基於CPU的litecoin挖礦環境便搭建好了。下面說怎麼用GPU（顯卡）來挖礦。
GPU挖礦 

對於GPU挖礦，除了運行軟件的不同，第一步和第三步都是一樣的。我們需要GUIminner來進行萊特幣的顯卡挖礦。GUIminner的萊特幣挖礦程序可以點擊這裡下載。
為了方便，我們繼續用上面coinotron的賬號。打開GUIminner，將自己的礦工名字和礦工密碼輸進去，端口輸入3334，調到適合自己電腦的GPU參數即可運行。




作者：P2PBUCKS ,轉載請註明出處並保持文章完整
 http://www.tshopping.com.tw/thread-233131-1-1.html