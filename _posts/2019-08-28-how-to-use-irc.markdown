---
layout: post
title:  "IRC 使用"
date:   2019-08-28 18:26:44 +0800
categories: irc
---

雖然對irc的起源並不是非常的理解，但是看到有非常非常多的超大型開源項目，都是透過都是透過這個聊天協議作為討論的平臺。譬如比特幣項目,Linux foundation,hack in Taiwan conference,Tor project,維基百科,Mozilla firefox。當然還有很多非常著名的頻道，那我就不一一列舉了。
要進入到Irc 有幾個步驟,要到這個項目的官方網站尋找他是否有開設Irc的頻道。如果有的話，那就可以去尋找，他是在哪一臺服務器上面搭建他的頻道？通常Irc的服務器都會有網絡的介面，方便一般使用者操作。

第一，尋找項目的官方lrc頻道的網站。
第二, 進入到網站之後。思考一下你要取什麼名字？並且輸入就可以直接登錄。
第三，沒有意外的話你可以順利的聽到Irc的服務器。這個時候還沒有進到任何的頻道。現在就是前往該項目的聯絡頁面，尋找他們的頻道名稱，找到之後，回到你原本的網頁，輸入想進入的頻道。
此時此刻的你，雖然已經順利，進入到頻道了，可是你的賬號也衹是一個臨時賬號。因為從一開始就沒有設定密碼，也就代表說這個賬號不屬於任何人。你可以在下一次登錄的時候換另外一個名字。當然這個名字，也可能之後被人家註冊。
所以如果想要永久持有一個地址的話，那就必須完成種下來的程序。

## 簡介
登入個大server，註冊帳號，請把密碼跟email改一改
這邊常用的有
* [freenode-Bircoin](https://en.bitcoin.it/wiki/IRC_channels)
* freenode-mozilla
* [oftc-Tor](https://www.torproject.org/contact/)
* [mozilla-摩茲工寮](https://moztw.org/space/)




## 註冊
```
/msg NickServ REGISTER password youremail@example.com
```

之後可以準備去mailbox 收驗證碼再輸一次

## Riot

RIOT 本身會幫你輸入的nickname加上'[m]'的字符，所以不是本尊，也沒有密碼

![](https://i.imgur.com/2BsTjTm.png)


### 插曲
因為riot 上的所有irc頻道，應該都是用託管的方式開的，所以都會有聊天記錄保留，這點挺好的。不過並非所有頻道都會被保留，如#bitcoin頻道，雖然曾經連線過，但好像脫線了。
![](https://i.imgur.com/Mz3I1ge.png)

### rito IRC 機器人大全
RIOT 中的 IRC 機器人，幫助你登入個大server
https://github.com/matrix-org/matrix-appservice-irc/wiki/Bridged-IRC-networks

### RIOT 番外篇 對接 Telegram 群
如果已經有telegram群了，希望可以在matrix發展，可以用機器人串起來。
https://t2bot.io/telegram/
他會幫你把riot群裡面的訊息，以機器人的方式轉送到tg群。（所以看到機器人在說話，不過會附註一下平台上的riot上的user name。圖片的話就更尷尬了。
![](https://i.imgur.com/X3DArfm.png)

### RIOT 番外篇 對接 Telegram 帳號

在對街群的過程中，會意外的把 telegram的帳號直接綁定到 riot上，使得riot可以直接跟 tg所有用戶說話。但所有聯絡人必須得到riot客戶端批准才會收到信息。


## 展示
順利的看到 bitcoin core 的大大們
![](https://i.imgur.com/12AU5VT.png)
