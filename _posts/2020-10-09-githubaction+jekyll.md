---
layout: post
title: "github action + jekyll"
date: 2020-10-9
tags: [github action]
categories: [github action]
image: image/github-action-6.png
description: ""
---

![](/image/github-action-6.png)

[TOC]

## 取得 github action token
* 取得新的 token [https://github.com/settings/tokens/new](https://github.com/settings/tokens/new)
![](/image/github-action-3.png)


## 輸入 輸入token 到該目標倉庫
* 網頁點擊： settings >> secrets

![](/image/github-action-1.png)

## 插入github action 腳本
* 在`.github/workflows`創建`run.yml`文件
* 插入以下[程式碼](https://jekyllrb.com/docs/continuous-integration/github-actions/)：

```
name: Build and deploy Jekyll site to GitHub Pages

on:
  push:
    branches:
      - master

jobs:
  github-pages:
    runs-on: ubuntu-16.04
    steps:
      - uses: actions/checkout@v2
      - uses: helaili/jekyll-action@2.0.1
        env:
          JEKYLL_PAT: ${{ secrets.JEKYLL_PAT }}
```

## 執行結果
![](/image/github-action-2.png)


## debug 插曲
### gem 套件版本問題
在本地端編譯都不是問題，但是在github action 編譯過程中卻遇到gem  版本不符的問題。
```
Starting the Jekyll Action
Your Gemfile has no gem server sources. If you need gems that are not already on
your machine, add a line like this to your Gemfile:
source 'https://rubygems.org'
Your bundle is locked to public_suffix (1.5.3), but that version could not be
found in any of the sources listed in your Gemfile. If you haven't changed
sources, that means the author of public_suffix (1.5.3) has removed it. You'll
need to update your bundle to a version other than public_suffix (1.5.3) that
hasn't been removed in order to install.
```
**問題解決**
在`Gemfile`文件第一行添加來源，即可解決
```
source 'https://rubygems.org'
```

### github action market 最多人在用的 aaction 不能用
[https://github.com/marketplace/actions/jekyll-actions](https://github.com/marketplace/actions/jekyll-actions)這是在market 最多人在用的版本，但該版本有致命的問題，無法自動部署 gh-pages 分支。
作者也說這有問題：
![](/image/github-action-4.png)
我嘗試了很久沒有看到問題的解決方案....
![](/image/github-action-5.png)

**問題解決**
直接換一個github action 程式碼吧
[https://jekyllrb.com/docs/continuous-integration/github-actions/](https://jekyllrb.com/docs/continuous-integration/github-actions/) 這是由jekyll 官方網站提供的版本。**成功可以運作**

## 參考文獻
* [https://jekyllrb.com/docs/continuous-integration/github-actions/](https://jekyllrb.com/docs/continuous-integration/github-actions/)
* [https://jekyllrb.com/docs/continuous-integration/github-actions/](https://jekyllrb.com/docs/continuous-integration/github-actions/)
* [https://github.com/marketplace/actions/jekyll-actions](https://github.com/marketplace/actions/jekyll-actions)