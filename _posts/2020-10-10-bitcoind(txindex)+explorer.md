---
layout: post
title: "bitcoind(txindex) + rpc explorer"
date: 2020-10-10
tags: [bitcoin]
categories: [bitcoin]
image: /image/bitcoind.png
description: ""
---

![](/image/bitcoind.png)

## bitcoind(txindex)
1. bitcoind 跑一個
2. 設定一下bitcoin.conf (`\AppData\Roaming\Bitcoin`) [bitcoin/bitcoin](https://github.com/bitcoin/bitcoin/blob/master/share/examples/bitcoin.conf)

```
txindex=1
server=1
rpcport=8332
rpcuser=username
rpcpassword=password
```

重啟
```
kill -9 -f bitcoind
./bitcoind -daemon
```

## btc-rpc-explorer
3. `npm install -g btc-rpc-explorer`
4. `btc-rpc-explorer -u username -w password -p 80 -i 0.0.0.0 --demo --rpc-allowall`

## todo
* https 可以搭配 caddy 使用

## 參考文獻
* [https://github.com/janoside/btc-rpc-explorer](https://github.com/janoside/btc-rpc-explorer)
* [https://github.com/janoside/btc-rpc-explorer/blob/master/.env-sample](https://github.com/janoside/btc-rpc-explorer/blob/master/.env-sample)