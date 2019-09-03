---
layout: post
title:  "Riot 整合 IRC, Telegram"
date:   2019-08-29 18:26:44 +0800
categories: [Riot]
tag: [IRC, matrixm, Riot, IRC]
image: image/riot1.png
---

在我理解上Riot是一個通信軟體的客戶端，又或者可以是一個品牌但實際上技術核心是[matrix 協議](https://github.com/matrix-org)。matrix 協議本身是開源的，內容相當複雜，好像牽涉到了一些去中心化協議，還也許多端點加密的選項。Riot 本身自帶一些聊天用戶客群，本身與telegram,facebook,twitter,IRC，互不相關的，但可以透過各種機器人，各種bridge把大家串起來。

- [Riot 相關連結：](#riot-%e7%9b%b8%e9%97%9c%e9%80%a3%e7%b5%90)
  - [客戶端](#%e5%ae%a2%e6%88%b6%e7%ab%af)
- [Riot 中的 IRC Channel](#riot-%e4%b8%ad%e7%9a%84-irc-channel)
  - [RIOT 自動幫你生成nickname 登入IRC](#riot-%e8%87%aa%e5%8b%95%e5%b9%ab%e4%bd%a0%e7%94%9f%e6%88%90nickname-%e7%99%bb%e5%85%a5irc)
  - [Riot 中 IRC bridge](#riot-%e4%b8%ad-irc-bridge)
  - [各大IRC server 大整合](#%e5%90%84%e5%a4%a7irc-server-%e5%a4%a7%e6%95%b4%e5%90%88)
  - [展示](#%e5%b1%95%e7%a4%ba)
- [Riot 登入自己的 IRC nickname](#riot-%e7%99%bb%e5%85%a5%e8%87%aa%e5%b7%b1%e7%9a%84-irc-nickname)
- [Riot 登入 Telegram](#riot-%e7%99%bb%e5%85%a5-telegram)
  - [Riot 番外篇 對接 Telegram 帳號](#riot-%e7%95%aa%e5%a4%96%e7%af%87-%e5%b0%8d%e6%8e%a5-telegram-%e5%b8%b3%e8%99%9f)

# Riot 相關連結：
* [matrix 協議的客戶端列表](https://matrix.org/docs/projects/try-matrix-now):這列表多到爆炸。
* Bridge[[1](https://matrix.org/bridges)], [[2](https://github.com/matrix-org/matrix-appservice-bridge)]:簡言之就是各種聊天軟體大串連，通通存到Matrix去。不過Bridge的概念是一個中繼器，假設我們想連IRC。
```
結構:
[IRC server]<--->[Bridge server]<--->[matrix server]
```
這個Bridge 會帶代替matrix server 使得用戶24小時 在線上，使得你不會遺失任何的聊天記錄。
實際上它提供了不只是IRC的Bridge，如下圖所示：
![](/image/riot1.png)


## 客戶端
以下是我個人偏好：
* ios : https://matrix.org/docs/projects/client/riot-ios
* android : https://github.com/vector-im/riotX-android
* mac os : https://riot.im/download/desktop/

# Riot 中的 IRC Channel

## RIOT 自動幫你生成nickname 登入IRC
在登入Riot的同時，Riot會全自動的幫你註冊IRC的Nickname（如果看不懂nickname是啥，看這[IRC 註冊筆記](https://awesome-doge.github.io/how-to-use-irc/))，這nickname的來源是你註冊的帳號底下的*用戶名*(如果沒做多餘的用戶名重設，應該就是帳號名)。
而Riot會自動幫你把你輸入的*用戶名*加上'[m]'的字符，生成`用戶名+ [m]`的一個nickname出來，幫你登入。因為IRC的帳號可以不註冊所以你會登入成功。

## Riot 中 IRC bridge
基本上可以讓你在Riot中看到這麼多頻道，都是因為Riot都幫你街上他們自行搭建的IRC bridge， IRC bridge 隨時保持在線上，所以他會幫我們保存所有的聊天記錄。

ps. 對IRC不熟的可能還要覺得很奇怪，為啥要刻意提起24hr在線，幫你保存聊天記錄，是因為IRC要在線上且進入頻道才可以搜集聊天記錄，如果離線的時間收到訊息都是看不到的，你只能去備份找。

## 各大IRC server 大整合
Riot 會自動幫你連入個大IRC server，還幫你整理的票票亮亮的一個聊天室搜尋引擎。左邊是搜尋引擎的結果，右邊是支持的 IRC bridge，要要Riot有列出來IRC bridge 才可以連線喔。
![](/image/irc1.png)

**IRC bridge 中的 channel掉線**：    
遇過有進到 freednode，但我卻找不到喜歡的 `#bitcoin`頻道，也是可以直接輸入`#bitcoin`強制進入。但是意外的發現是，聊天室內跟真正的freenode上的bitcoin頻道斷線了，所以變成bridge channel裡面的人在自嗨。
因為Riot 上的所有IRC channel。
![](/image/irc2.png)

## 展示
順利的看到 bitcoin core 的大大們.   
![](/image/irc4.png)

# Riot 登入自己的 IRC nickname
這時有很多人做了IRC Bridge，做了很棒的 IRC 機器人讓你好好登入自己的nickname。
[機器人列表](https://github.com/matrix-org/matrix-appservice-IRC/wiki/Bridged-IRC-networks)

準備：你必須要在各大平台註冊過nickname取得密碼後再來。
1. 找你高興的機器人，如我像好好登入freenode，機器人叫做`@appservice-irc:matrix.org`
2. 在Riot中跟他開房間聊天，邀請他`@appservice-irc:matrix.org`
3. 他不會主動理你，你需要跟他說話。我們要來打註冊的指令，指令不難理解，把awesome-doge換成你自己註冊過的有密碼的nickname。
```
!nick awesome-doge
```
enter 之後，他會告訴你他幫你把名字換成你指定的nickname勒
```
Nick changed from 'awesome-doge[m]' to 'awesome-doge'.
```
這時候不用再跟他聊天了，沒他的事了。
4. 會挑出一個新的機器人跟你聊天，跟你要密碼如下
```
This nickname is registered. Please choose a different nickname, or identify via /msg NickServ identify <password>.
```
你回答只需要`identify <password>`就可以勒。恭喜大大


# Riot 登入 Telegram
如果已經有telegram群了，希望可以在matrix發展，可以用[t2bot機器人](https://t2bot.io/telegram/)串起來。他會幫你把Riot群裡面的訊息，以機器人的方式轉送到tg群。（所以看到機器人在說話，不過會附註一下平台上的Riot上的user name。圖片的話就更尷尬了。

![](/image/irc3.png)

## Riot 番外篇 對接 Telegram 帳號

在對街群的過程中，會意外的把 telegram的帳號直接綁定到 Riot上，使得Riot可以直接跟 tg所有用戶說話。但所有聯絡人必須得到Riot客戶端批准才會收到信息。