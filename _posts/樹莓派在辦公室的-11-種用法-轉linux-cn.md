---
title: '樹莓派在辦公室的 11 種用法 [轉linux.cn]'
date: 2018-12-27 15:06:32
tags: [linux.cn, Raspberry Pi]
categories: linux.cn
---

樹莓派在辦公室的 11 種用法 [轉linux.cn]

我知道你在想什麼：樹莓派只能用在修修補補、原型設計和個人愛好中。它實際不能用在業務中。

毫無疑問，這臺電腦的處理能力相對較低、易損壞的 SD 卡、缺乏電池備份以及支援的 DIY 性質，這意味著它不會是一個能在任何時候執行最關鍵的操作的專業的、已安裝好、配置好的商業伺服器的可行替代品。

但是它電路板便宜、功耗很小、小到幾乎適合任何地方、無限靈活 —— 這實際上是處理辦公室一些基本任務的好方法。

而且，更好的是，已經有一些人完成了這些項目並很樂意分享他們是如何做到的。

<!-- more --> 

## DNS 伺服器
每次在瀏覽器中輸入網站地址或者點選連結時，都需要將域名轉換為數字 IP 地址，然後才能顯示內容。

通常這意味著向網際網路上某處 DNS 伺服器發出請求 —— 但你可以通過本地處理來加快瀏覽速度。

你還可以分配自己的子域，以便本地訪問辦公室中的計算機。

[這裡瞭解它是如何工作的](https://www.1and1.com/digitalguide/server/configuration/how-to-make-your-raspberry-pi-into-a-dns-server/)。

## 廁所佔用標誌
在廁所排過隊嗎？

這對於那些等待的人來說很煩人，花在處理它上面的時間會耗費你在辦公室的工作效率。

我想你希望在辦公室裡也懸掛飛機上那個廁所有人的標誌。

[Occu-pi](https://blog.usejournal.com/occu-pi-the-bathroom-of-the-future-ed69b84e21d5) 是一個非常簡單的解決方案，使用磁性開關和樹莓派來判斷螺栓何時關閉，並在 Slack 頻道中更新“廁所在使用中” —— 這意味著整個辦公室的人都可以看一眼電腦或者移動裝置知道是否有空閒的隔間。

## 針對黑客的蜜罐陷阱
黑客破壞了網路的第一個線索是一些事情變得糟糕，這應該會嚇到大多數企業主。

這就是可以用到蜜罐的地方：一臺沒有任何服務的計算機位於你的網路，將特定埠開啟，偽裝成黑客喜歡的目標。

安全研究人員經常在網路外部部署蜜罐，以收集攻擊者正在做的事情的資料。

但對於普通的小型企業來說，這些作為一種絆腳石部署在內部更有用。因為普通使用者沒有真正的理由想要連線到蜜罐，所以任何發生的登入嘗試都是正在進行搗亂的非常好的指示。

這可以提供對外部人員入侵的預警，並且也可以提供對值得信賴的內部人員的預警。

在較大的客戶端/伺服器網路中，將它作為虛擬機器執行可能更為實用。但是在無線路由器上執行的點對點的小型辦公室/家庭辦公網路中，[HoneyPi](https://trustfoundry.net/honeypi-easy-honeypot-raspberry-pi/) 之類的東西是一個很小的防盜報警器。

## 列印伺服器
聯網印表機更方便。

但更換所有印表機可能會很昂貴 —— 特別是如果你對現有的印表機感到滿意的話。

[將樹莓派設定為列印伺服器](https://opensource.com/article/18/3/print-server-raspberry-pi)可能會更有意義。

## 網路附加儲存（NAS）
將硬碟變為 NAS 是樹莓派最早的實際應用之一，並且它仍然是最好的之一。

[這是如何使用樹莓派建立 NAS](https://howtoraspberrypi.com/create-a-nas-with-your-raspberry-pi-and-samba/)。

## 工單伺服器
想要在預算不足的情況下在服務檯中支援工單？

有一個名為 osTicket 的完全開源的工單程式，它可以安裝在你的樹莓派上，它甚至還有[隨時可用的 SD 卡映象](https://everyday-tech.com/a-raspberry-pi-ticketing-system-image-with-osticket/)。

## 數字標牌
無論是用於活動、廣告、選單還是其他任何東西，許多企業都需要一種顯示數字標牌的方式 —— 而樹莓派的廉價和省電使其成為一個非常有吸引力的選擇。

[這有很多可供選擇的選項](https://blog.capterra.com/7-free-and-open-source-digital-signage-software-options-for-your-next-event/)。

目錄和資訊亭
[FullPageOS](https://github.com/guysoft/FullPageOS) 是一個基於 Raspbian 的 Linux 發行版，它直接引導到 Chromium 的全屏版本 —— 這非常適合導購、圖書館目錄等。

基本的內聯網 Web 伺服器
對於託管一個面向公眾的網站，你最好有一個託管帳戶。樹莓派不適合面對真正的網路流量。

但對於小型辦公室，它可以託管內部業務維基或基本的公司內網。它還可以用作沙箱環境，用於試驗程式碼和伺服器配置。

[這裡是如何在樹莓派上執行 Apache、MySQL 和 PHP](https://maker.pro/raspberry-pi/projects/raspberry-pi-web-server)。

## 滲透測試器
Kali Linux 是專為探測網路安全漏洞而構建的作業系統。通過將其安裝在樹莓派上，你就擁有了一個超行動式穿透測試器，其中包含 600 多種工具。

[你可以在這裡找到樹莓派映象的種子連結](https://www.offensive-security.com/kali-linux-arm-images/)。

絕對要小心只在你自己的網路或你有權對它安全審計的網路中使用它 —— 使用此方法來破解其他網路是嚴重的犯罪行為。

## VPN 伺服器
當你外出時，依靠的是公共無線網際網路，你無法控制還有誰在網路中、誰在窺探你的所有流量。這就是為什麼通過 VPN 連線加密所有內容可以讓人放心。

你可以訂閱任意數量的商業 VPN 服務，並且你可以在雲中安裝自己的服務，但是在辦公室執行一個 VPN，這樣你也可以從任何地方訪問本地網路。

對於輕度使用 —— 比如偶爾的商務旅行 —— 樹莓派是一種強大的，節約能源的設定 VPN 伺服器的方式。（首先要檢查一下你的路由器是不是不支援這個功能，許多路由器是支援的。）

[這是如何在樹莓派上安裝 OpenVPN](https://medium.freecodecamp.org/running-your-own-openvpn-server-on-a-raspberry-pi-8b78043ccdea)。

## 無線咖啡機
啊，美味：好喝的飲料是神賜之物，也是公司內工作效率的支柱。

那麼，為什麼不將辦公室的[咖啡機變成可以精確控制溫度和無線連線的智慧咖啡機](https://www.techradar.com/au/how-to/how-to-build-your-own-smart-coffee-machine)呢？

原文：[https://linux.cn/article-10375-1.html](https://linux.cn/article-10375-1.html)