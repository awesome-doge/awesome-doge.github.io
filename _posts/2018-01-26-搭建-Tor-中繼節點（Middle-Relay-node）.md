---
layout: post
title: 搭建 Tor 中繼節點（Middle Relay node）
date: 2018-01-26 19:28:57
tags: [tor, tor relay, hidden, tor v2, tor v3,anonymous]
categories: [Tor Project]
---

![](/image/tor18.png)

在洋蔥網路中有分目錄節點（Directory node）、入口節點（EntryGguard node）、中繼節點（Middle Relay node）、出口節點（Exit Relay node）。也有各式各樣的網橋技術主要是為了避過網路審查，如obfs3、obfs4、meek之類。進入洋蔥網路要先到目錄節點尋找入口（多個）、中繼（多個）、出口（多個）節點資訊，本地端會隨機挑選入口、中繼、出口節點形成一條路徑。

<!-- more --> 

目錄節點好像不是一般人可以搭建，入口、出口節點太明顯容易被攻擊或是被喝茶，所以今天說的是中繼節點。

### 一、前置作業

Mac：

1. 請先安裝brew
2. 之後執行 brew install tor
3. 執行完一次看到100%可以先control+c 咖掉

windows：

1. 到Tor Project[1]下載Expert Bundle
2. 下載完之後壓縮到你喜歡的地方
3. 進到Tor資料夾，點擊Tor.exe，完整運行看到100% 可以關掉了

Ubuntu/Debian：

1. sudo apt-get install tor
2. terminnal 執行 tor ，看到100% 可以control+c 咖掉

### 二、接下來配置Torrc文件

最新版的原始Torrc 配置文件在此[2]

> 各個版本的配置文件位置
> Mac：/usr/local/etc/tor/torrc
> Windows：%appdata%\tor\torrc
> Ubuntu/Debian：/etc/tor/torrc

ps : 如果沒有文件的用記事本創一個，不要有副檔名喔

### 修改torrc

新增以下描述，可以自行修改。之後儲存

```
ORPort 443
Exitpolicy reject *:*
Nickname Bitcoiner #自己取一個喜歡的名字 我是Bitcoiner
ContactInfo ***@gmail.com #輸入自己的email
AccountingMax 500 GBytes # 每月分配给Tor 500G 流量
AccountingStart month 3 15:00 # 每月3号15点(Locale)清零
RelayBandwidthRate 100 KBytes # Throttle traffic to 100KB/s (800Kbps) 
RelayBandwidthBurst 200 KBytes # But allow bursts up to 200KB (1600Kb)
```

### 三、運行

>各個版本運行
>Mac：tor
>Windows：執行 tor資料夾底下的tor.exe
>Ubuntu/Debian：tor

ps. 因為需要port 443 請自行調整防火牆規則

### 四、觀測

![](/image/tor19.png)

我是還沒看見我自己的，不過應該夠久（三小時），就會出現在Tor Metrics[3] 觀測站，可以輸入剛剛在修改 torrc時設定的Nickname，應該可以搜尋得到。這是我的[6]

![](/image/tor20.png)

ps 看到最上面藍色框框了嗎？他說我目前不能直接提供 洋蔥網路作為中繼需要透過時間的歷練，歷練的標準原文[7]中文翻譯[8]
[1]https://www.torproject.org/download/download.html.en

[2]https://raw.githubusercontent.com/torproject/tor/master/src/config/torrc.sample.in

[3]https://atlas.torproject.org

[4]https://blog.jxtsai.info/2017/06/14/torrelay/

[5]https://yepster.me/tor-deployment/

[6]https://atlas.torproject.org/#details/C9BFA7484D05A2FCF72D2286F455201B8D5E9743

[7]https://blog.torproject.org/lifecycle-new-relay

[8]https://blog.jxtsai.info/2017/06/22/torrelay-2/
