---
layout: post
title:  "Riot中的IRC"
date:   2019-08-29 18:26:44 +0800
categories: IRC
tag: IRC, telegram, matrixm Riot
---

在我理解上Riot是一個通信軟體的客戶端，又或者可以是一個品牌但實際上技術核心是matrix 協議。matrix 協議本身是開源的，內容相當複雜，好像牽涉到了一些去中心化協議，還也許多端點加密的選項。Riot 本身自帶一些聊天用戶客群，本身與telegram,facebook,twitter,IRC，互不相關的，但可以透過各種機器人，各種bridge把大家串起來。

Riot 相關連結：
* [matrix 協議的客戶端列表](https://matrix.org/docs/projects/try-matrix-now):這列表多到爆炸。
* [Bridge](https://matrix.org/bridges):最不知道是不是刻意勒，狂做bridge。簡言之就是各種聊天軟體大串連，通通存到Matrix去。不過Bridge的概念是一個中繼器，假設我們想連IRC，結構:`[IRC server]<--->[Bridge server]<--->[matrix client]`，這個Bridge 會帶代替matrix client 使得用戶24小時 在線上，使得你不會遺失任何的聊天記錄。


## Riot 中的IRC Channel
Riot 本身與IRC Channel 整合的不錯，自己搭建了一大堆
Riot 本身會幫你輸入的nickname加上'[m]'的字符，所以不是本尊，也沒有密碼

![](/image/irc1.png)


### 插曲
因為Riot 上的所有IRC channel ，應該都是用託管的方式開的，所以都會有聊天記錄保留，這點挺好的。不過並非所有 channel 都會被保留，如#bitcoin channel ，雖然曾經連線過，但好像脫線了。    
![](/image/irc2.png)

### rito IRC 機器人大全
Riot 中的 IRC 機器人，幫助你登入個大server
https://github.com/matrix-org/matrix-appservice-IRC/wiki/Bridged-IRC-networks

### Riot 番外篇 對接 Telegram 群
如果已經有telegram群了，希望可以在matrix發展，可以用機器人串起來。
https://t2bot.io/telegram/
他會幫你把Riot群裡面的訊息，以機器人的方式轉送到tg群。（所以看到機器人在說話，不過會附註一下平台上的Riot上的user name。圖片的話就更尷尬了。    
![](/image/irc3.png)

### Riot 番外篇 對接 Telegram 帳號

在對街群的過程中，會意外的把 telegram的帳號直接綁定到 Riot上，使得Riot可以直接跟 tg所有用戶說話。但所有聯絡人必須得到Riot客戶端批准才會收到信息。


## 展示
順利的看到 bitcoin core 的大大們.   
![](/image/irc4.png)