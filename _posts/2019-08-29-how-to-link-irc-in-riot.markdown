---
layout: post
title:  "Riot中的IRC"
date:   2019-08-29 18:26:44 +0800
categories: IRC
---

> 在我理解上Riot是一個通信軟體的客戶端，又或者可以是一個品牌但實際上技術核心是matrix 協議。matrix 協議本身是開源的，內容相當複雜，好像牽涉到了一些去中心化協議，還也許多端點加密的選項。Riot 本身自帶一些聊天用戶客群，本身與telegram,facebook,twitter,IRC，互不相關的，但可以透過各種機器人，各種bridge把大家串起來。


## Riot 中的IRC Channel
Riot 本身與IRC Channel 整合的不錯。
Riot 本身會幫你輸入的nickname加上'[m]'的字符，所以不是本尊，也沒有密碼

![](https://i.imgur.com/2BsTjTm.png)


### 插曲
因為Riot 上的所有IRC channel ，應該都是用託管的方式開的，所以都會有聊天記錄保留，這點挺好的。不過並非所有 channel 都會被保留，如#bitcoin channel ，雖然曾經連線過，但好像脫線了。    
![](https://i.imgur.com/Mz3I1ge.png)

### rito IRC 機器人大全
Riot 中的 IRC 機器人，幫助你登入個大server
https://github.com/matrix-org/matrix-appservice-IRC/wiki/Bridged-IRC-networks

### Riot 番外篇 對接 Telegram 群
如果已經有telegram群了，希望可以在matrix發展，可以用機器人串起來。
https://t2bot.io/telegram/
他會幫你把Riot群裡面的訊息，以機器人的方式轉送到tg群。（所以看到機器人在說話，不過會附註一下平台上的Riot上的user name。圖片的話就更尷尬了。    
![](https://i.imgur.com/X3DArfm.png)

### Riot 番外篇 對接 Telegram 帳號

在對街群的過程中，會意外的把 telegram的帳號直接綁定到 Riot上，使得Riot可以直接跟 tg所有用戶說話。但所有聯絡人必須得到Riot客戶端批准才會收到信息。


## 展示
順利的看到 bitcoin core 的大大們.   
![](https://i.imgur.com/12AU5VT.png)