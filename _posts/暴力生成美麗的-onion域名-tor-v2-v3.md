---
title: 暴力生成美麗的.onion域名(tor v2 & v3)
date: 2018-01-19 17:01:44
tags: [tor, onion address]
categories: Tor Project
---

說是暴力一點都不奇怪，重述.onion的域名生成是private key>(rsa)>public key>(sha1)>雜湊值>(base32編碼)>得到很醜的地址.onion。這道理跟比特幣生成特定地址是同樣的[3]，但是因為計算量太大所以大家都會折衷，只要地址前幾位有個人特色就好，不然要算到幾千萬年喔(時間評估表放在本文最下方)。


所以原理是，要不斷的一值嘗試不同的private key輸入，看看有沒有你要的結果，例如Facebook的洋蔥地址"facebookcorewwwi.onion"[2]是不是很美，要爆破這麼多位，我看也只有Facebook做得到，因為在密碼學上的評估要暴力解出這樣的結果以 1.5Ghz Processor要 2.6 million years，驚為天人Facebook秀肌肉展現它有龐大運算sha1的驚人實力。這也意味著這是Facebook本尊啦。

![](/image/tor6.jpeg)
<!-- more --> 

以下提供我搜尋完的暴力嘗試美麗名稱的倉庫，說的蠻清楚的：

>katmagic/Shallot：應該算是早期的版本，用CPU慢慢算
>lachesis/scallion：開始有人覺得不夠快啦，通通改寫成GPU啦
>cathugger/mkp224o：因為大家都開始意識到rsa、sha1快要撐不下去了，在今年一月十號左右tor project表示，新的洋蔥v3將會有ecc ，而這個倉庫是以v3 的協議 去做的 爆破

ps 如果爆破缺了什麼 套件沒辦法跑可以裝一下“sudo apt-get install libssl-dev”

忘記說了，爆破完的結果，會生成private key 跟 public key ，這時我們芷絮要到，上一篇文章[1]中提到的" HiddenServiceDir"中的private key檔案修改成新的，並且把public key刪掉。再進到解壓縮出來的tor資料夾，運行tor.exe，這時應該都成功了，新的網址會在” HiddenServiceDir”中的publickey文件出現，如果跟預期的不一樣有機會試privatekey手殘貼錯。

![](/image/tor7.png)

[1]https://medium.com/%40pwchen/%E6%90%AD%E5%BB%BAtor-%E4%B8%AD%E7%9A%84-onion-%E7%B6%B2%E7%AB%99-9551c43b3adb

[2]https://en.wikipedia.org/wiki/Facebookcorewwwi.onion

[3]https://en.bitcoin.it/wiki/Vanitygen
