---
layout: post
title:  "構建電子書＆網站 by gitbook"
date:   2019-08-26 17:26:44 +0800
categories: [Gitbook]
tag: [gitbook, github, github hompage]
---

gitbook 是一個命令工具，幫助你把一堆`md`,`asciidoc`build 成網頁版的電子書以及mobi, epub, pdf的檔案生成。

閱讀該文章時[markdown](https://gist.github.com/christech1117/6dc5221c177104990767d6490ad8c7ba) 語法是基本常識。
![](/images/gitbook.jpg)

因為最近不斷地整理電子書，發現了電子書的遍及格式大致有`markdown`格式，簡稱`md`，還有另外一種叫`asciidoc`，我初次見到到`asciidoc`是在[bitcoinbook](https://github.com/bitcoinbook/bitcoinbook)之後又遇見了[ethereumbook](https://github.com/ethereumbook/ethereumbook)，可是裡面的公式還是呈現不出來，後來遇見了gitbook，讓我很舒服的把`md`,`asciidoc` build 成網頁版的電子書以及mobi, epub, pdf 三種格式，讓大家可以在手機上就可閱讀。

gitbook 的使用過程:
  * 安裝：安裝所需的指令環境。
  * build ： 生成網頁的電子書文件。
  * gitbook 伺服：器運行一個gitbook 伺服器，讓你可以在 http://localhost:4000 的位置，喵一下樣子。
  * 編譯成書籍 mobi, epub, pdf 。

## 安裝 gitbook 指令
如果沒有安裝過gitbook的可以執行一下
ps. gitbook 依賴npm，npm的安裝請參考[node js 下載頁面](https://nodejs.org/en/download/)自己安裝加油嘿。   
![](/images/node.js.png)

務必要安裝完才可以執行以下指令安裝`gitbook`，不然無效。
安裝也是需要一些時間。
```
sudo npm install -g gitbook-cli
sudo npm install -g gitbook
```
## 製作一本書
現在我們來創造一個名字你高興的資料夾（建議是英文書名），進去之後，指行以下指令初始化一下該資料夾（這可能會花一點時間）。
```
gitbook init
```

執行的過程，跑完恭喜你：
```
➜  ~ mkdir book
➜  ~ cd book
➜  book gitbook init
warn: no summary file in this book
info: create README.md
info: create SUMMARY.md
info: initialization is finished
```
裡面會有兩個檔案，分別為`README.md`,  `SUMMARY.md`。

## 書本結構
`SUMMARY.md`文件定義了整本書的結構。
結構很簡單，就是一個簡單的markdown語法的清單。
```
# Summary

* [Introduction](README.md)
* [第一章](ch1.md)
	* [第一節](ch1-1.md)
	* [第二節](cd1-2.md)
* [第二章](ch2.md)
* [第三章](ch3.md)
```

## build
執行該指令可以把`SUMMARY.md`引用到的文件，變成網頁。
```
gitbook build
```

build的過程，此時，資料夾內會多一個`_book`資料夾，裡面就是創見出來的網頁：
```
➜  book gitbook build
info: 7 plugins are installed
info: 6 explicitly listed
info: loading plugin "highlight"... OK
info: loading plugin "search"... OK
info: loading plugin "lunr"... OK
info: loading plugin "sharing"... OK
info: loading plugin "fontsettings"... OK
info: loading plugin "theme-default"... OK
info: found 1 pages
info: found 0 asset files
info: >> generation finished with success in 1.2s !
```

## 運行 伺服器模式
運作成伺服器，可以即時瀏覽書籍撰寫的變化，`gitbook serve`會隨時偵測你存擋，刷新網頁。

```
gitbook serve
```
運行成功如下，就可以前往[http://localhost:4000](http://localhost:4000)瀏覽：
```
Starting server ...
Serving book on http://localhost:4000
```

## 製作成電子書

gitbook 可以製作書籍種類
```
gitbook pdf
gitbook epub
gitbook mobi
```
如果覺得懶，已可以寫一個`build-book.sh`把以程式碼貼上去，以後只要`sh build-book.sh 書名`就可以自動生成勒。

```
gitbook pdf $1
gitbook epub $1
gitbook mobi $1
```
### 問題
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

先前準備：
* 在 gitbub上創建一個repo
* 把它clone 到 local 端
* 進到 該資料夾 初始化變成書 `gitbook init`（已經是書的不要理我

### 開始發布
進到github clone 下來的 repo

1. 先做一下手腳（這是為了可以讓自動化發布網頁鋪路）：
	* 在 主目錄創一個 文件 叫`.gitignore`
	* 內容如下
	```
	*~
	_book
	.DS_Store
	```
	* 來`gitbook build`一下，刷新`_book`內容
	* 來推到主分之一下避免衝突
	```
	git commit -am "update"; git add . ;git push origin master
	```
2. 創建一個分支叫做`gh-pages`，這個執行一次就好
	```
	git checkout --orphan gh-pages
	```
3. 進到`gh-pages`分支
	* 移除主目錄下根本不是網頁的檔案，如果沒有做第一步的，你屎定了，文件全部都會消失。
	```
	git rm --cached -r .
	git clean -df
	```
	* 把`_book`裡面的文件複製出來
	```
	cp -r _book/* .
	```
	* 堆一波到`gh-page`分支
	```
	git commit -am "update"; git add . ;git push origin gh-pages
	```
	* 可以回到主目錄勒，如果不知道怎麼回家的
	```
	git checkout master%
	```
* 檢查一下有沒有發布成功，網址的樣子要是`帳號名稱.github.io/倉庫名稱`，譬如`https://cypherpunks-core.github.io/bitcoinbook_2nd_zh/`，祝您旅途愉快。


### 自動發布腳本
請在主目錄建立一個文件叫`publish.sh`，把下面內容貼上並存擋。
執行`sh publish.sh '更新的說明'`就可以勒。
```
git checkout master
gitbook build 
git add .
git commit -m $1
git push -u origin master
git branch -D gh-pages
git branch  -r -d  origin/gh-pages
git push origin :gh-pages
git checkout --orphan gh-pages
git rm --cached -r .
git clean -df
cp -r _book/* .
git add .
git commit -m $1
git push -u origin gh-pages
git checkout master%
```

### 常見問題
問. 我發佈啦，怎麼無法在`帳號名稱.github.io/倉庫名稱`域名下看到我的網站勒？
* 要等一段時間（看運氣），幾秒鐘到三分鐘不等
* 你檢查一下你有推到 `gh-pages`分支嗎？
* 既使你推到了`gh-pages`分支，你有順利的把`_book`中的網頁拉出來嗎？最少要`index.html`
* 該 repo 的setting 選項當中，有一個預設branch 的選項，檢查一下是否設定在`gh-pages`分支。

## 參考文獻
* [gitbook——使用笔记](https://morrowind.gitbooks.io/gitbook_notes/content/qian_yan.html)
* [GitBook文档（中文版）](https://chrisniael.gitbooks.io/gitbook-documentation/content/index.html)
* [Gitbook 安装及使用 ](https://my.oschina.net/lpe234/blog/854226)
* [Mac上将gitbook转化成pdf文档下载](https://www.jianshu.com/p/6a16064a4d1e)
* [自动化脚本](https://yangjh.oschina.io/gitbook/UsingPages.html)