---
layout: post
title:  "IRC 註冊筆記"
date:   2019-08-28 18:26:44 +0800
categories: [IRC]
tag: [IRC]
image: images/irc-demo.png
description: "要參與一些大型開源項目，加入IRC是第一步"
---

雖然對IRC的起源並不是了解的太多，但是看到有非常非常多的超大型開源項目，都是透過都是透過這個聊天協議作為討論的平臺。譬如比特幣項目,Linux foundation,hack in Taiwan conference,Tor project,維基百科,Mozilla firefox。當然還有很多非常著名的 channel ，那我就不一一列舉了。

![](/images/irc-demo.png)

要進入到IRC 有幾個步驟,要到這個項目的官方網站尋找他是否有開設IRC的 channel 。如果有的話，那就可以去尋找，他是在哪一臺伺服器上面搭建他的 channel ？通常IRC的伺服器都會有網絡的介面，方便一般使用者操作。

1. 尋找項目IRC頻道頁面：尋找項目的官方IRC channel 的網站。如[freenode-Bitcoin](https://en.bitcoin.it/wiki/IRC_channels)，在這個頁面當中就展示了跟比特幣相關的IRC channel，頁面當中有提供網頁版，對小白友善一點。
比較著名的IRC channel：
	* [freenode-Bitcoin](https://en.bitcoin.it/wiki/IRC_channels)
	* [freenode-mozilla](https://wiki.mozilla.org/IRC)
	* [oftc-Tor](https://www.torproject.org/contact/)
	* [mozilla-摩茲工寮](https://moztw.org/space/)
	* [freenode-維基百科](https://meta.wikimedia.org/wiki/IRC/Channels)
2. 設定nickname：進入到網站之後。思考一下你要取什麼名字？並且輸入就可以直接登錄。完全不需要密碼，現在那nick name就是你的身份啦。
3. 尋找channel：沒有意外的話你可以順利的聽到IRC的伺服器。這個時候還沒有進到任何的 channel 。現在就是前往該項目的聯絡頁面，尋找他們的 channel 名稱，以Bitcoin 為例，最多人的是bitcoin chainnel。找到之後，回到你原本的網頁，輸入想進入的 channel 。。
> 此時此刻的你，雖然已經順利，進入到 channel 了，可是你的賬號也衹是一個臨時賬號。因為從一開始就沒有設定密碼，也就代表說這個賬號不屬於任何人。你可以在下一次登錄的時候換另外一個名字。當然這個名字，也可能之後被人家註冊。所以如果想要永久持有一個地址的話，那就必須完成種下來的程序。
4. 進入之後，會有一個channel不是頻道，那頻道是跟伺服器聊天。我們就在這裡註冊帳號嘍！
註冊帳號的指令，：`/msg NickServ REGISTER `的部分不變，後面自己發揮，也不要亂填黑，這是要拿來收電子郵件驗證碼的。
```
/msg NickServ REGISTER password youremail@example.com
```
5. 完成第四部之後順利的話你會在信箱中收到一封郵件，裡面也是一行指令，不又多想把他複製貼上到IRC 的伺服器頻道就對了。`enter`恭喜你跳出驗證通過啦。

**小結**：現在這帳號歸你所有啦，得說清楚，一個帳號一個伺服器，看到網址不依樣的都要重新註冊，註冊的方法大同小異，有些根本不用收email。