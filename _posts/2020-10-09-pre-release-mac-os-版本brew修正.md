---
layout: post
title: "pre release mac os 版本 brew 修正"
date: 2020-10-9
tags: [brew]
categories: [brew]
image: /image/xcode-select.png
description: "brew 對 xcode-select  有很強的依賴，所以必須尋找xcode-select 的beta版本以解決該問題。"
---

最近很熱情裝了 mac os beta版本，結果許多brew update,brew install 遇到許多問題，因為brew 對 xcode-select  有很強的依賴，所以必須尋找xcode-select 的beta版本以解決該問題。

**問題**
可以看到`xcrun:`那列 系統是滿頭問號的
```
~  brew config
HOMEBREW_VERSION: 2.5.5-19-g87942d1
ORIGIN: https://github.com/Homebrew/brew
HEAD: 87942d17482d41568ef3c10b71a1196c08305a1c
Last commit: 70 minutes ago
Core tap ORIGIN: https://github.com/Homebrew/homebrew-core
Core tap HEAD: 62667b011c5f166af0285955de56c4672f6b0145
Core tap last commit: 39 minutes ago
Core tap branch: master
HOMEBREW_PREFIX: /usr/local
HOMEBREW_CASK_OPTS: []
HOMEBREW_MAKE_JOBS: 4
Homebrew Ruby: 2.6.3 => /usr/local/Homebrew/Library/Homebrew/vendor/portable-ruby/2.6.3_2/bin/ruby
CPU: quad-core 64-bit kabylake
xcrun: error: invalid active developer path (/Library/Developer/CommandLineTools), missing xcrun at: /Library/Developer/CommandLineTools/usr/bin/xcrun
Clang: N/A
Git: 2.28.0 => /usr/local/bin/git
Curl: 7.64.1 => /usr/bin/curl
macOS: 11.0-x86_64
CLT: N/A
Xcode: 12.2 => /Applications/Xcode-beta.app/Contents/Developer
```
**安裝gcc 失敗的慘況**
```
brew install gcc
Warning: You are using macOS 11.0.
We do not provide support for this pre-release version.
You will encounter build failures with some formulae.
Please create pull requests instead of asking for help on Homebrew's GitHub,
Discourse, Twitter or IRC. You are responsible for resolving any issues you
experience while you are running this pre-release version.
```
**網路上查到說要安裝xcode-select**，但是系統跳出來的所有安裝版本都是正式版本，測試版的mac os 無法正常安裝
```
xcode-select --install
xcode-select: note: install requested for command line developer tools
```
## 解決方案
前往 [https://developer.apple.com/download/more/](https://developer.apple.com/download/more/) 下載需要的版本 Command_Line_Tools_for_Xcode_12.2_beta_2.dmg 安裝他

![](/image/xcode-select.png)


**結果可以跑了**
```
~ brew install gcc
Updating Homebrew...
Warning: You are using macOS 11.0.
We do not provide support for this pre-release version.
You will encounter build failures with some formulae.
Please create pull requests instead of asking for help on Homebrew's GitHub,
Discourse, Twitter or IRC. You are responsible for resolving any issues you
experience while you are running this pre-release version.

==> Downloading https://homebrew.bintray.com/bottles/gcc-10.2.0.catalina.bottle.tar.gz
==> Downloading from https://d29vzk4ow07wi7.cloudfront.net/8dbccea194c20b1037b7e8180986e98a8ee3e37eaac12c7d223c89be3deaac6a?res
######################################################################## 100.0%
==> Pouring gcc-10.2.0.catalina.bottle.tar.gz
🍺  /usr/local/Cellar/gcc/10.2.0: 1,463 files, 338.7MB
```