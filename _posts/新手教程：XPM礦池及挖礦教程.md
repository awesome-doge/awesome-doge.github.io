---
title: 新手教程：XPM礦池及挖礦教程
date: 2014-08-29 20:12:53
tags: [blogger, primecoin, pool, miner]
categories: Blogger
---

Primecoin簡稱XPM，中文名為質數幣。該幣發佈以後，憑藉其全新的創意和對數學學術界帶來的貢獻，引起了電子錢行業極大的關注，幾日間，用戶數量飆升，其貨幣價格一路看漲，當前的價格折合人民幣已經達到2元左右，這對一個新幣來說十分難得。 

<!-- more --> 

質數幣簡介： 

Primecoin發佈於2013年7月7日,目前只能用cpu挖，且挖礦軟體即為錢包軟體。XPM總量不設上限，根據未來素數的出現而提高。每分鐘1個塊，每個區塊產量取決於破解質數的難度。 

XPM官方網站：http://primecoin.org 


XPM用戶端錢包： 

http://sourceforge.net/projects/primecoin/files/latest/download?source=files 


XPM礦池： 

http://ypool.net 


挖礦方法： 

1.打開網站→點擊“Register”(註冊) 

2.點擊“Workers”，註冊礦工，礦工名稱為註冊時的用戶名，默認尾碼為.xpm1，密碼為x，可不改，如有更改請按“Update”(更新) 

3.點擊“How to”，下載此礦池XPM的專用挖礦軟體，點擊“jhPrimeminer v0.21 download” 

4.下載解壓後，資料夾內只有一個“jhPrimeminer.exe”檔，在這個資料夾裡，新建一個批次檔(尾碼為.bat)，具體方法為：先新建一個TXT文字檔，然後複製以下文字到這個文字檔 

jhPrimeMiner.exe -o http://ypool.net:8332 -u 網站註冊用戶名.xpm1 -p x 

需要改的內容有“網站註冊用戶名” ，尾碼或密碼也有更新，也按更新後的更改。保存後，在此文字檔上右鍵點“重命名”，將副檔名.txt改為.bat 

5.按兩下運行此BAT檔，即可實現挖礦。會同步顯示每個CPU核的速度及難度。 

6.如幾台電腦同時挖礦，請註冊不同礦工。 


XPM用戶端挖礦方法： 

下載PrimeCoin錢包用戶端，同步完資料包才能開始挖礦。然後點擊“Help”，再點擊“Debug Window”，然後切換到控制台，在控制台下方的輸入setgenerate true，回車，開始挖礦。或者'setgenerate true <thread-limit> thread-limit為執行緒數。如果是兩執行緒就 setgenerate true 2 , 其他類推。如果散熱良好，你就直接 setgenerate true ,全速挖。 

輸入getmininginfo查看挖礦狀態 

單獨挖礦收益不穩定。


XPM交易網站：
http://bter.com/