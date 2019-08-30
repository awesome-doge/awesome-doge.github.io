---
layout: post
title: Android Bitcoin Wallet 於2013年 不隨機
date: 2018-01-28 05:12:19
tags: [bitcoin]
categories: Bitcoin Technical
---

導致 55.82BTC 被駭

在Bitcoin 系統中，所有Bitcoin 餘額的載體對我來說應該就是地址了。

那地址是如何生成的呢，只要記得有一個亂數產生的私鑰，經過一個不可逆的計算會生出地址。那亂數產生夠不夠隨機，這便是攸關比特幣到底會不會被偷走啊。大家或許會覺得今天創建一個新的錢包會不會有機會隨機生成一個跟別人一模一樣的種子，或許在現在不可能。

但在2013年的8月這件事情是可能的。因為在Android的亂數產生器並不隨機導致，比特幣的私要不隨機，導致大家可能建構出一模一樣的wallet。有些攻擊者就開始測試到底會不會撞到別人生成的地址。

<!-- more --> 

比特幣的開發者也發現了這樣的疏失也在2013年8月發表了公開信[3]，希望大家解決這樣的嚴重漏洞。也有許多相關的新聞[1]

**“All private keys generated on Android phones/tablets are weak and some signatures have been observed to have colliding R values, allowing the private key to be solved and money to be stolen,”**

### Bitcoin.org 發布

Bitcoin.org有發佈了正式的警告[2]，只要用本地端的亂數產生器都會受到影響，並指出受到影響的包括Bitcoin Wallet、BitcoinSpinner、Mycelium Bitcoin Wallet、blockchain.info。

![](/image/b1.png)

### Android 回覆
那問題本是誰，那就是Android 本身啦，他們也知道自己是比特幣被盜事件的元兇ＸＤ。[4]

>We have now determined that applications which use the Java Cryptography Architecture (JCA) for key generation, signing, or random number generation may not receive cryptographically strong values on Android devices due to improper initialization of the underlying PRNG.

### 對使用者而言帶來多大的影響呢？
這是Bitcoin talk 上面的討論[5]，説看得見的55.82多BTC，但這是檯面上，檯面下就不知道了ＸＤ

![](/image/b2.png)

[1]https://www.csoonline.com/article/2133842/data-protection/bitcoin-wallets-on-android-at-risk-of-theft--developers-say.html

[2]https://bitcoin.org/en/alert/2013-08-11-android

[3]https://threatpost.com/bitcoin-transactions-on-android-vulnerable-to-theft/101958/

[4]https://android-developers.googleblog.com/2013/08/some-securerandom-thoughts.html

[5]https://bitcointalk.org/index.php?topic=271486.0
