---
layout: post
title: "Firefox+SwitchyOmega+onion"
date: 2020-03-14
tags: [tor, hidden, tor v3,anonymous, proxy, firefox]
categories: [Tor Project]
image: /image/ProxySwitchyOmega.png
description: ""
---

本文將以firefox為基礎，設置proxy 規則，讓 .onion 地址 走 tor routin，一般地址正常上網。
![](/image/ProxySwitchyOmega.png)

純粹使用tor browser 有以下問題：
* cookie 每次重新開啟都會被刪除，導致每次都要重新登入
* 許多網站對 tor ip 很不友善，一直要求圖靈驗證
* 也不是每個網站都需要 tor routing

## 搭建 tor socks 5 代理
安裝
```
for debian/ubuntu
sudo apt-get tor

for mac os
brew install tor
```

運行
```
tor
```
執行後不關就行

畫面如下
![](/image/tor34.png)

## 安裝 browser 擴展套件
