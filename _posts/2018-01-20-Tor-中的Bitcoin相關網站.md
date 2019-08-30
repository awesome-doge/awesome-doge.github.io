---
layout: post
title: Tor 中的Bitcoin相關網站
date: 2018-01-20 17:14:09
tags: [tor, bitcoin]
categories: [Tor Project]
---

因為研究Bitcoin 在這裡分享一下在洋蔥裡面，其實也有許多知名的比特幣網站，搭建的洋蔥網站（這裡先不提洗錢或是賭場ＸＤ），以下網頁都需要使用Tor Browser瀏覽[1]：

### Zcash官網
zcash是一個密碼貨幣，他與比特幣不同的是他可以加密部分交易，使得大家可以選擇性公開讓大家來看交易內容，與門羅幣不同的是，門羅是全部加密的，zcash也是可以不加密。

洋蔥網址：http://zcashph5mxqjjby2.onion/

![](/image/tor8.png)

<!-- more --> 

### GreenAddress
這技術是基於比特幣的多重簽章技術，簡單的說他把一個地址的持有把原本的一把private key ，以hash的方法使得它可以拆成多把，再給他一個參數說，在這麼多把key當中要同時以幾把驅動才可以使得交易成立。那多重簽章技術在GreenAddress中，是把private key拆成兩把，一把是使用者持有，一把是GreenAddress持有，在交易發起的過程中，需要使用者簽署完成，送到GreenAddress在簽一次才可以廣播交易。而GreenAddress的簽署，是以一個第三方公正的方式，去保證他簽署過的地址不會是“雙花攻擊”，使得收款的商家可以安心的接受“零確認交易”。

洋蔥網址：http://s7a4rvc6425y72d2.onion/en/
![](/image/tor9.png)

### blockchain.info
這是一個老字號的比特幣區塊鏈檢視器網站，也有自己的錢包服務，做了許多區塊鏈的分析並且畫成圖表。

洋蔥地址：https://blockchainbdgpzk.onion/
![](/image/tor10.png)

### reddit/bitcoin
嚴格來說這是一個論壇，但是這論壇討論比特幣的程度比bitcointalk來得踴躍很多。這網站因為很注重個人隱私，所以也讓很注重隱私的tor用戶願意在這裡開版。

洋蔥地址：http://redditmoongroogs.onion/r/Bitcoin/
![](/image/tor11.png)

[1]https://www.torproject.org/projects/torbrowser.html.en#downloads-alpha
