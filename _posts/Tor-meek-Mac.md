---
title: Tor + meek (Mac)
date: 2018-02-01 19:28:57
tags: [tor, meek]
categories: Tor Project
---

emmm…會寫這一篇呢，主要是因為某些環境下，在``brew install tor``還有``tor``跑起來之後，並無法順利的抵達Tor directory server，也就無法進一步提取一些中繼節點來建立路徑。

![卡在連線 Tor directory server](/image/tor28.png)

<!-- more --> 

Tor Project 為了可以讓用戶順利的抵達Tor directory server，開發了許多方法使用戶可以順利抵達。這些方法被Tor Project稱之為Pluggable Transports，方法有許多包括​obfs4（之所以是4，也就是說有1,2,3啦，只是都退役了）、meek（簡單的來說就是將流量重新包裝成https的樣子，在封包辨識上比較難辨別）….等，當中每個在包裝技術都很有趣包括，重新包裝成skype流量。

![just 參考](/image/tor29.jpeg)

回到Bash，本文將以Pluggable Transports中的meek嘗試是否可以順利訪問Tor directory server。在``brew install tor``之後，來clone一個meek工具（這是Tor Project 自己的git）下來：

```
git clone https://git.torproject.org/pluggable-transports/meek.git
```

接下來到/meek/meek-client 底下 執行`make`（前提是要裝好go，有些不足的go包報錯會有載點）一下，順利的話 你會跟我依樣見到一個meek-client

![](/image/tor30.png)

接下來把這個meek-client 丟到/usr/local/etc/tor 下。

![](/image/tor31.png)

接下來ㄋㄟ，要來編輯一下/usr/local/etc/tor/torrc，不需要sudo 直接打開編輯，在最上面加入些訊息包括，要用bridge, 要連到哪個bridge, 要用meek插件，具體如下，改完之後儲存。至於要用哪一個bridge 這邊是以AZURE為例。

```
UseBridges 1
Bridge meek 0.0.2.0:3 url=https://meek.azureedge.net/ front=ajax.aspnetcdn.com
ClientTransportPlugin meek exec ./meek-client — log meek-client.log
```

最後一步，在終端裡面，執行`tor`就行了。

### 可能的錯誤
但是ㄋㄟ ，之前的我常常遇到既使都設定對了還是跑不出來主要報錯如下：

![](/image/tor32.png)

這時我是把/usr/local/etc/tor中的log 砍了 就意外過了23333

參考文獻

[1]https://trac.torproject.org/projects/tor/wiki/doc/PluggableTransports/list#PTlibraries

[2]https://www.slideshare.net/antitree/meek-and-domain-fronting-public