---
layout: page
title: "Post"
permalink: /post/
---



**2020/10/23**    
隨著GLV 橢圓曲線(這可以加速33%的效能) 專利過期 差不多一個月了   ，GLV也已經Merge 到 bitcoin/bitcoin，原本不明白為啥可以寫這麼快，原來是sipa 早已寫好 沒公布

With the GLV elliptic curve (which can speed up the performance by 33%), the patent has expired for almost a month, and GLV has also been merged to bitcoin/bitcoin. I didn’t know why sipa could be written so fast. It turns out that sipa has already completed the code, but it hasn't been announced.
效能測試

[https://github.com/bitcoin/bitcoin/pull/20147#issuecomment-711051877](https://github.com/bitcoin/bitcoin/pull/20147#issuecomment-711051877)

---

**2020/10/23**    
一個預防日蝕攻擊的措施，重啟節點連線時先連到原先連過的節點
* [https://github.com/bitcoin/bitcoin/pull/17428](https://github.com/bitcoin/bitcoin/pull/17428)
* [https://github.com/bitcoin/bitcoin/pull/17428#issuecomment-578500393](https://github.com/bitcoin/bitcoin/pull/17428#issuecomment-578500393)


Bitcoin Core #17428 writes a file at shutdown with the network addresses of the node’s two outbound block-relay-only peers. The next time the node starts, it reads this file and attempts to reconnect to those same two peers. This prevents an attacker from using node restarts to trigger a complete change in peers, which would be something they could use as part of an eclipse attack that could potentially trick the node into accepting invalid bitcoins.

---

**2020/10/23**    

Satoshi 一開始用 Berkeley DB，這版本從2010年至今沒人更新，既使要更動也是程式崩潰。最近因為導入了新的descriptor  錢包，順便塞進去一個SQLite。沒想到開發者們竟然又再度發起了移除Berkeley DB的計畫。但計畫會到2023年底會完工。

Satoshi first used Berkeley DB. No one has updated this version since 2010. Even if it needs to be changed, the program crashes. Recently, because of the introduction of a new descriptor wallet, a SQLite was inserted by the way. Unexpectedly, the developers once again launched a plan to remove Berkeley DB. But it is planned to be completed by the end of 2023.

[https://github.com/bitcoin/bitcoin/issues/20160](https://github.com/bitcoin/bitcoin/issues/20160)

---

**2020/10/23**   

Bitfinex 是一個早期投入閃電網路的交易所，最近它支援了Wumbo(鉅額閃電網路通道標準)

Bitfinex is an early exchange that invested in the Lightning Network, and recently it supports Wumbo (Huge Lightning Network Channel Standard)

[https://blog.bitfinex.com/trading/bitfinex-supports-the-lightning-networks-wumbo-channels/](https://blog.bitfinex.com/trading/bitfinex-supports-the-lightning-networks-wumbo-channels/)

---

**2020/10/23**   

blockstream 區塊鏈瀏覽器開發出閃電網路版本了，不過看起來烙賽中


The blockstream blockchain explorer has developed a version of the Lightning Network, but it looks like it’s in the race
[https://github.com/lvaccaro/esplora_clnd_plugin](https://github.com/lvaccaro/esplora_clnd_plugin)

---

**2020/10/23**   

bluewallet 支援了 Payjoin ，使交易更匿名
[https://blockstream.com/2018/08/08/en-improving-privacy-using-pay-to-endpoint/](https://blockstream.com/2018/08/08/en-improving-privacy-using-pay-to-endpoint/)

