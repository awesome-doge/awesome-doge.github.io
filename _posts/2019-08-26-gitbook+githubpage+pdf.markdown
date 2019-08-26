---
layout: post
title:  "Bitcoin 的閱讀清單"
date:   2019-08-26 18:26:44 +0800
categories: bitcoin
---

因為已經用了各種不成熟的方法在撰寫書籍，所以精進一下製作工藝。
本篇將簡單說明
* 原來gitbook 是一個指令
  * 安裝
  * 編譯
  * 運行一個伺服器
  * 編譯成書籍 包括pdf 

## gitbook 安裝

如果沒有安裝過gitbook的可以執行一下
ps. npm的問體自己加油嘿，提示node及npm
```
sudo npm install -g gitbook-cli
sudo npm install -g gitbook
```
## 初始化一本書
```
gitbook build
```

## 編譯
去生一個書籍出來，進入到ripo
```
gitbook build
```
運作成伺服器
```
gitbook serve
```

## 製作成電子書

gitbook 可以製作書籍種類
```
gitbook pdf
gitbook epub
gitbook mobi
```

不過如果你直接使用會遇到以下報錯：
```
InstallRequiredError: "ebook-convert" is not installed.
Install it from Calibre: https://calibre-ebook.com
```
解決方法：
* 前往 https://calibre-ebook.com/download ，下載mac 的版本
* 安裝它，把他丟到`應用程式`裡面
* 執行以下指令:
```
sudo ln -s /Applications/calibre.app/Contents/MacOS/ebook-convert /usr/local/bin
```
ok，應該可以很舒服的執行勒

## 參考文獻
* [gitbook——使用笔记](https://morrowind.gitbooks.io/gitbook_notes/content/qian_yan.html)
* [GitBook文档（中文版）](https://chrisniael.gitbooks.io/gitbook-documentation/content/index.html)
* [Gitbook 安装及使用 ](https://my.oschina.net/lpe234/blog/854226)
* [Mac上将gitbook转化成pdf文档下载](https://www.jianshu.com/p/6a16064a4d1e)