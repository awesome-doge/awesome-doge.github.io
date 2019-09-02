---
layout: post
title: "Jekyll 搭建 github page"
image: /image/jekyll1.png
date: 2019-08-31
tags: [jekyll]
categories: [jekyll]
---

如果今天想要搭建一個Blog或是個人網站甚至是一個公司產品的網站，卻又懶得去租用一個VPS伺服器，這篇文章會是一個不錯的教學。因為其實每一個人的github都可以搭建成一個靜態網站，而每一個repo都可以搭建成子網站，換言之。可以在這樣子的github page架構下搭建很多很多很多的網站。

- [環境搭建](#%e7%92%b0%e5%a2%83%e6%90%ad%e5%bb%ba)
- [生成網站](#%e7%94%9f%e6%88%90%e7%b6%b2%e7%ab%99)
  - [無中生有初始化一個網站](#%e7%84%a1%e4%b8%ad%e7%94%9f%e6%9c%89%e5%88%9d%e5%a7%8b%e5%8c%96%e4%b8%80%e5%80%8b%e7%b6%b2%e7%ab%99)
  - [github page](#github-page)
    - [現成模板](#%e7%8f%be%e6%88%90%e6%a8%a1%e6%9d%bf)
      - [分叉 變成 主網頁](#%e5%88%86%e5%8f%89-%e8%ae%8a%e6%88%90-%e4%b8%bb%e7%b6%b2%e9%a0%81)
      - [分叉 變成 子網頁](#%e5%88%86%e5%8f%89-%e8%ae%8a%e6%88%90-%e5%ad%90%e7%b6%b2%e9%a0%81)
- [`_config.yml`文件修調整](#configyml%e6%96%87%e4%bb%b6%e4%bf%ae%e8%aa%bf%e6%95%b4)
- [`_post` 資料夾](#post-%e8%b3%87%e6%96%99%e5%a4%be)
- [build 出 靜態網站文件](#build-%e5%87%ba-%e9%9d%9c%e6%85%8b%e7%b6%b2%e7%ab%99%e6%96%87%e4%bb%b6)
  - [本地server](#%e6%9c%ac%e5%9c%b0server)
    - [自動發布 github page](#%e8%87%aa%e5%8b%95%e7%99%bc%e5%b8%83-github-page)
- [Markdown 語法](#markdown-%e8%aa%9e%e6%b3%95)
- [進階](#%e9%80%b2%e9%9a%8e)
  - [圖片大小、位置控制](#%e5%9c%96%e7%89%87%e5%a4%a7%e5%b0%8f%e4%bd%8d%e7%bd%ae%e6%8e%a7%e5%88%b6)
  - [表格欄位內的換行](#%e8%a1%a8%e6%a0%bc%e6%ac%84%e4%bd%8d%e5%85%a7%e7%9a%84%e6%8f%9b%e8%a1%8c)
  - [數學公式](#%e6%95%b8%e5%ad%b8%e5%85%ac%e5%bc%8f)
  - [任務列表](#%e4%bb%bb%e5%8b%99%e5%88%97%e8%a1%a8)
- [參考文獻](#%e5%8f%83%e8%80%83%e6%96%87%e7%8d%bb)


# 環境搭建
在搭建網站之前，我們需要先設定好我們的環境，這樣才可以執行jekyll運作起來我們的部落格或是網站。
主要依賴 `gem`指令，他好像是ruby。但我使用的是mac os 他本身自帶。剩下需要做的事`gem install jekyll`

# 生成網站
##  無中生有初始化一個網站
在當前目錄下生成一個`blog`資料夾，並前初始化為靜態網站
```
jekyll new blog
```
進去之後運行 `jekyll serve`就可以在[http://127.0.0.1:4000](http://127.0.0.1:4000) 或是 [http://localhost:4000](http://localhost:4000)看到最乾淨的網站了。

## github page
來到我一個最重要的一步，我們中了伺服器不是為了在本地端開一個伺服器出來。是為了能夠生成一個文件丟到github上面，進一步讓我變成一個靜態的網頁託管。
這是我們開始一個repo，命名為`xxx.github.io` 這邊的xxx是你賬戶註冊所使用的用戶名稱，衹要有一點點的差異就是不會成功了。現在我們把這個repoClone 下來，再把我們剛剛申請的所有的靜態網站，全部丟進去。做一個 add commit push基本上再過不久的時間，你就可以看到他了。他會出現在`xxx.github.io`在網址當中。通常需要最快30秒，最長差不多四五分鐘的反應時間。他並不會立刻馬上的出現在你的網頁上面。

### 現成模板
因為在jekyll已經不是什麼小項目了，他已經存在了非常多年，所以也會有許多熱情的開發者撰寫了很多公開的模板給大家使用，[http://jekyllthemes.org](http://jekyllthemes.org)，如果在裡面有你看起來高興的樣子，就可以直接拿來用，直接`fork`一個很快的。這樣可以省去很多開發時間，也對一個小白是非常友善的。
所以如果挑到喜歡的，那就讓我們分叉一個吧。
![](/image/jekyll1.png)

#### 分叉 變成 主網頁
github會給每個user 一個網址，只是看你有沒有拿來用而已，預設是`xxx.github.io`，其中xxx是你自己的名字。
你只要把你`fork`出來的repo，點擊該repo頁面的右上角的setting ，重新命名該repo為`xxx.github.io`的格式，過個幾分鐘你就可以進到`xxx.github.io`的網站了。

#### 分叉 變成 子網頁
子網頁是指我們不是`xxx.github.io`，我們把網頁搭載`xxx.github.io/repo名稱`，這是你`fork`完，依樣把repo 重新命名一下，應該就要在`xxx.github.io/repo名稱`下看到自己的內容了。如果沒看到可以檢查一下repo中的setting，下面會有GitHub Pages 相關的設定，可能是因為為他就線在其他的分支了。
> 補充說明 通常我們會把 生成靜態網頁前的原始碼放在 master 分支，把生成玩的靜態網頁放在gh-pages分支。不知哪來的傳統，不過現在github 設定裡面也支持，指定要用哪個branch呈現網頁的選項。

![](/image/jekyll4.png)

# `_config.yml`文件修調整
會來到這裡，就代表著你已經從模板庫裡面找到了一個不錯的網站做樣本。可是你從模板庫裡面拿到了網站，裡面預設的信息基本上都是別人家的blog或是公司，所以現在我們要把它變成自己的網頁，我們要來修改我們自己的個人信息，那麼裡面的詳細細節，每一個模板都會有不太一樣，所以建議大家還是一一的看一下自己的檔案慢慢的修改，它裡面都一定會有提示。

# `_post` 資料夾
這是一個資料夾這是博客文章的地方。
![](/image/jekyll5.png)
基本上每一個文件頂部有詳細的要求，如果並文章內的YAML頭部沒有按照這樣子的規則去撰寫的話，它會完全無法識別。

在預設的情況下，這個資料夾裡面本來就會存放一些文章。你可以大概學習一下別人大概是怎麼樣去撰寫一篇文章的。
基本上每一個文章的開頭都有詳細的YAML的格式設定。當中比較特別的是第一行`layout: post`，這邊定義了呈現的頁面樣式，而頁面樣式在`_layouts`資料夾中有詳細的定義。

<div align="center"><img  src="/image/jekyll6.png"/></div>

# build  出 靜態網站文件
會走到這裡代表你的`_config`文件已經設定完成，還有已經設定好一些文章可以發佈了，即使沒有文章也沒關係。

這個時候我們進到總目錄底下執行`jekyll build` 就可以順順利利的製作一個網站出來。如果順利運作成功的話，你可以在目錄底下看到很多html的文件。在其中，index.html最為重要，因為它是流覽你網頁的第1個頁面。
所以現在你有Index.html的文件了。這時的你可以嘗試用瀏覽器看，看看這個文件，看看是否順利的可以開起來。
![](/image/jekyll2.png)

## 本地server
當我們製作好，文件夾好，其實jekyll同時也支持伺服器。你衹要在根目錄底下執行`jekyll serv` 你就會在本地端啟動一個伺服器出來。這個伺服器是HTTP的伺服器，同時它也會開啟一個4000端口出來。所以你這時開啟一個瀏覽器輸入[http://127.0.0.1:4000](http://127.0.0.1:4000) 或是 [http://localhost:4000](http://localhost:4000) 就可以順利的造訪這個網頁。
值得一提的是，這個伺服器是隨時更新的，他會無時無刻，偵測你在資料夾裡面的檔案變動。他衹要一發現有一些檔案被修改了，他就會立刻去重新建立一個新的網頁出來。而且執行的速度非常快，他可以讓你在最快的時間內看到你的網頁變化。
![](/image/jekyll3.png)

### 自動發布 github page
為了使得發布更加的快速，做了自動 add, commit, push 的腳本
首先在目錄底下執行 `nano publish.sh`，創建一個文黨貼上去，contral+o儲存，contral+x退出
```
jekyll build; git commit -am $1 ; git add . ;git push origin master
```
使用方法`sh publish.sh "更新的commit message"`，就會自動更新勒。

# Markdown 語法

# 進階
## 圖片大小、位置控制
[來自[這裡](https://mazhuang.org/2017/09/01/markdown-odd-skills/)]    
**預設的圖片效果：**    
原始碼：
```
![](/images/doge.png)
```
![](/images/doge.png)

**大小、位置控制：**    
原始碼：
```
<div align="center"><img width="65" height="75" src="/images/doge.png"/></div>
```
<div align="center"><img width="65" height="75" src="/images/doge.png"/></div>
## 表格欄位內的換行
[來自[這裡](https://mazhuang.org/2017/09/01/markdown-odd-skills/)]    
範例程式碼：    
```
| Header1 | Header2                          |
|---------|----------------------------------|
| item 1  | 1. one<br />2. two<br />3. three |
```

效果：  
  
| Header1 | Header2                          |
|---------|----------------------------------|
| item 1  | 1. one<br />2. two<br />3. three |


## 數學公式
[來自[這裡](https://mazhuang.org/2017/09/01/markdown-odd-skills/)]    
如果是在 GitHub Pages，可以參考 http://wanguolin.github.io/mathmatics_rending/ 使用 MathJax 來優雅地展示數學公式（非圖片）。

如果是在 GitHub 項目的 README 等地方，目前我能找到的方案只能是貼圖了，以下是一種比較方便的貼圖方案：

1. 在 [https://www.codecogs.com/latex/eqneditor.php](https://www.codecogs.com/latex/eqneditor.php) 網頁上部的輸入框裡輸入 LaTeX 公式，比如 `$$x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}$$`。

2. 在網頁下部拷貝 URL Encoded 的內容，比如以上公式生成的是 `https://latex.codecogs.com/png.latex?%24%24x%3D%5Cfrac%7B-b%5Cpm%5Csqrt%7Bb%5E2-4ac%7D%7D%7B2a%7D%24%24`。

3. 在文檔需要的地方使用以上 URL 貼圖，比如:
原始碼：
```
![](https://latex.codecogs.com/png.latex?%24%24x%3D%5Cfrac%7B-b%5Cpm%5Csqrt%7Bb%5E2-4ac%7D%7D%7B2a%7D%24%24)
```
效果：    
![](https://latex.codecogs.com/png.latex?%24%24x%3D%5Cfrac%7B-b%5Cpm%5Csqrt%7Bb%5E2-4ac%7D%7D%7B2a%7D%24%24)

## 任務列表
[來自[這裡](https://mazhuang.org/2017/09/01/markdown-odd-skills/)]    
在 GitHub 和 GitLab 等網站，除了可以使用有序列表和無序列表外，還可以使用任務列表，很適合要列出一些清單的場景。
原始碼：
```
**購物清單**

- [ ] 一次性水杯
- [x] 西瓜
- [ ] 豆漿
- [x] 可口可樂
- [ ] 小茗同學
```

效果： 

**購物清單**

- [ ] 一次性水杯
- [x] 西瓜
- [ ] 豆漿
- [x] 可口可樂
- [ ] 小茗同學

# 參考文獻
* [官網連結](https://jekyllrb.com/docs/)
* [簡體中文官網](https://jekyllcn.com)
* [关于 Markdown 的一些奇技淫巧](https://mazhuang.org/2017/09/01/markdown-odd-skills/)