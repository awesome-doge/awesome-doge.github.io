---
layout: post
title: "tor v3 hidden service 設定 + ssh 連線"
date: 2020-03-11
tags: [tor, hidden, tor v3,anonymous]
categories: [Tor Project]
image: /image/tor33.png
description: "搭建hidden service、搭建hidden ssh、連線hidden ssh"
---

搭建hidden service、搭建hidden ssh、連線hidden ssh
![](/image/tor33.png)

## server setting

### 1個 hidden address service
0. 安裝 tor ： `sudo apt-get install tor`
    * 因為會背景執行，查一下PID`sudo lsof -i | grep LISTEN`
    * 殺掉他 `sudo kill <pid>`
2. 修改`/etc/tor/torrc`
    ```
    HiddenServiceDir /home/<username>/<hiddenfile_A>
    HiddenServicePort 22 127.0.0.1:22
    ```
    * HiddenServiceDir ：可設定到 `/home/<username>/<hiddenfile_A>`
        * 修改一下權限，不然不讓跑：`sudo chmod 700 /home/<username>/<hiddenfile_A>`
    * left port : hidden port
    * right port : 本機 port

2. 跑起來 執行 `tor`
    > 會自動在`/home/<username>/<hiddenfile_A>` 生成三個文件，分別為 私鑰、公鑰、地址，需要將地址分享出去。

### 多個 hidden address service

1. 修改`/etc/tor/torrc`
    ```
    HiddenServiceDir /home/<username>/<hiddenfile_A>
    HiddenServicePort 80 127.0.0.1:80

    HiddenServiceDir /home/<username>/<hiddenfile_B>
    HiddenServicePort 80 127.0.0.1:8080

    HiddenServiceDir /home/<username>/<hiddenfile_C>
    HiddenServicePort 80 127.0.0.1:8081
    ```
    * 不同的<hiddenfile_*>代表不同的hidden 網址，上例會生成三個網址(上線)，分別儲存在資料夾中的`hostname`
2. 跑起來 執行 `tor`
    > 換看到創建的資料夾都生成了私鑰、公鑰、地址


## ssh client setting
0. 在本地端先跑一個 `brew install tor`，執行`tor`
1. 修改 .ssh/config，添加以下內容
```
Host *.onion *-tor
  ProxyCommand nc -X 5 -x 127.0.0.1:9050 %h %p
  CheckHostIP  no
  Compression  yes
  Protocol     2
```

2. 可以連線了`ssh <username>@<hostname-onion>.onion`

參考文獻：https://blog.w1r3.net/2018/02/11/ssh-hidden-service.html

## 暴力生成 特殊 tor v3 address
> 成品展示 winnie `<winnienbkmomnlswyfwfrpv7nl3svncbsqsyizbwgt75kcorbp5d6uad.onion>`

下載
```
sudo apt-get install git
git clone https://github.com/cathugger/mkp224o.git
cd mkp224o
sudo apt install gcc libsodium-dev make autoconf
```
編譯
```
./autogen.sh
./configure
./configure CPPFLAGS="-I/usr/local/include" LDFLAGS="-L/usr/local/lib"
make
```
使用

> 注意：詞彙設定絕對不要太短(小於等於3字)，會生成太快造成硬碟毀損，或難以刪除
```
./mkp224o <詞彙_A> <詞彙_B> <...> 
```
* `-S 1` 顯示狀態，每秒一次，預設十秒刷新一次
* `-j 10` ：使用CPU數量，預設是全開
* `./mkp224o -h` : 更多內容說明

若有成果會出現在同一個資料夾中，以`<onionaddress>.onion`資料夾呈現，資料夾中會有私鑰、公鑰、地址，若要啟用則丟入`/home/<username>/<hiddenfile_*>`，覆蓋就行。

參考文獻：https://github.com/cathugger/mkp224o