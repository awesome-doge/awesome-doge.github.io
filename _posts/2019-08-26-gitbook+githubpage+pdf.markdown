---
layout: post
title:  "透過gitbook搭建githubpage＋生成電子書"
date:   2019-08-26 17:26:44 +0800
categories: gitbook, githubpage
tag: gitbook, github, github hompage
---

因為最近不斷地整理電子書，發現了電子書的遍及格式大致有`markdown`格式，簡稱`md`，還有另外一種叫`asciidoc`，我初次見到到`asciidoc`是在[bitcoinbook](https://github.com/bitcoinbook/bitcoinbook)之後又遇見了[ethereumbook](https://github.com/ethereumbook/ethereumbook)，可是裡面的公式還是呈現不出來，後來遇見了gitbook，讓我很舒服的把`md`,`asciidoc` build 成網頁版的電子書以及mobi, epub, pdf 三種格式，讓大家可以在手機上就可閱讀。

gitbook 是一個命令工具，幫助你把一堆`md`,`asciidoc`build 成網頁版的電子書以及mobi, epub, pdf生成。

gitbook 的使用過程:
  * 安裝：安裝所需的指令環境。
  * build ： 生成網頁的電子書文件。
  * gitbook 伺服：器運行一個gitbook 伺服器，讓你可以在 http://localhost:4000 的位置，喵一下樣子。
  * 編譯成書籍 mobi, epub, pdf 。



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

## 發佈到github page
創建一個分支，這個執行一次就好
```
git checkout -b gh-pages
```

以下是一個 自度發佈的腳本，可以創立一個`gitbook.sh`的檔案，可以一直更新
```
gitbook build
```

```
git checkout master
git add .
git commit -m $1
git push -u origin master
git checkout gh-pages
cp -r _book/* .
git add .
git commit -m $1
git push -u origin gh-pages
git checkout master
```
執行的時候在repo裡面
```
sh gitbook.sh '更新'
```


## 參考文獻
* [gitbook——使用笔记](https://morrowind.gitbooks.io/gitbook_notes/content/qian_yan.html)
* [GitBook文档（中文版）](https://chrisniael.gitbooks.io/gitbook-documentation/content/index.html)
* [Gitbook 安装及使用 ](https://my.oschina.net/lpe234/blog/854226)
* [Mac上将gitbook转化成pdf文档下载](https://www.jianshu.com/p/6a16064a4d1e)
* [自动化脚本](https://yangjh.oschina.io/gitbook/UsingPages.html)