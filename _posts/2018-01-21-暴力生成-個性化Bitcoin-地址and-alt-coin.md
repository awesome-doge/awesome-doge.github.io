---
layout: post
title: 暴力生成 個性化Bitcoin 地址and alt coin
date: 2018-01-21 17:53:01
tags: [tor, bitcoin, bitcoin address]
categories: [Tor Project]
---

用過比特幣的各位肯定會覺得，哇～比特幣地址好醜、這麼亂、這麼不好記，在這裡將大家說一個做個性化的Bitcoin地址的方法。如果不清楚比特幣地址如何生成，那只要記得，隨機生成一個亂數>>透過橢圓曲線算法算成公鑰>>之後透過各種雜湊函數算一下>>在用base58編成一個比較好看的樣子。看了這麼多還是不懂那就記得隨機生成一把私鑰，只會對應到一個地址（沒有辦法反推）。
![](/image/tor12.jpeg)

<!-- more --> 

要生成特殊的地址可以在samr7/vanitygen[1]中找到生成的腳本，本身支持不只是CPU計算，同時也支援了GPU，可以指定想要的地址前幾位，也不能選擇太多位因為越多位，所花的計算時間就會呈指數成長，詳見[2]，文中說道生成一個“1Bitcoin”開頭的地址要費時一週。

![](/image/tor13.png)

順便一提，後來發現基於samr7/vanitygen改寫的進階版exploitagency/vanitygen-plus[3]，這個進階版支持的貨幣相當多，較為著名的有Blackcoin、Bitcoin Testnet、Dash、DeepOnion、Dogecoin、Litecoin、Monacoin、Namecoin、Peercoin。

ps 這些生成方法，是否基於一個相當隨機的亂數產生器去建立，會直接影響到你地址安全性。我不知道這些作者的亂數產生器是否靠譜

[1]https://github.com/samr7/vanitygen

[2]https://en.bitcoin.it/wiki/Vanitygen

[3]https://github.com/exploitagency/vanitygen-plus
