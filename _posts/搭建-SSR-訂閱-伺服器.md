---
title: '搭建 SSR 訂閱 伺服器 '
date: 2019-01-06 20:39:31
tags: [ss, ssr]
---

學習 ss ,ssr 地址格式 >> 轉換為訂閱格式（僅支持ssr地址，要將ss轉為ssr）

## 瞭解ss,ssr 地址格式[原文](https://ntgeralt.blogspot.com/2018/06/ssr.html)

SS = ShadowSocks
SSR = ShadowSocksR

<!-- more -->

### ss 地址
ss連結的格式比SSR連結組成簡單一些很多很多，Base64編碼前的ss連結如下：
```
ss://method:password@server:port
```

一般我們見到的都是Base64編碼後的連結，格式如下：
```
ss://Base64編碼欄位
```

### ssr 地址

SSR連結未Base64編碼前格式如下：
```
ssr://server:port:protocol:method:obfs:password_base64/?suffix_base64
```

特殊的地方在於`password_base64/?suffix_base64`，從名字應該能看出來，這是兩個已經被Base64編碼的東西，一個是密碼，但那個`suffix_base64`是個什麼東西呢？
好吧，這其實是我隨便取的一個名字...它實際是一個包含`協議參數`、`混淆參數`、`群組名`、`備註(伺服器名)`的欄位。

該欄位未Base64編碼前格式如下：
```
/?obfsparam=obfsparam_base64&protoparam=protoparam_base64&remarks=remarks_base64&group=group_base64
```

我們平常見到的已經被Base64編碼的SSR連結是這樣的：
```
ssr://Base64編碼欄位
```
被Base64編碼的欄位就是
```
server:port:protocol:method:obfs:password_base64/?suffix_base64
```
這麼一大坨東西。

所以說SSR連結比SS連結複雜了很多啊啊啊，（摔

PS. 仔細閱讀的童鞋想必不難發現密碼，`協議參數`、`混淆參數`、`群組名`、`備註(伺服器名)`這一大堆東西都被Base64編碼了兩次 (再摔

PSS. 所以`decode`的時候記得長點心啊～～


額，沒錯，裡面的參數也被Base64編碼了……

## 將準備好的 ssr 地址轉換為 訂閱格式

1. 以下為demo 材料
```
ssr://MTM4LjEyOC4yMTkuMTgxOjYxMjM0OmF1dGhfc2hhMV92NDphZXMtMjU2LWNmYjp0bHMxLjJfdGlja2V0X2F1dGg6WTJ4dmRXUm1jbUV1WTI5dC8_b2Jmc3BhcmFtPSZyZW1hcmtzPU0tV1B0dyZncm91cD01THFSNTZ1djVxR0c1cDYy
ssr://MjMuODguMjM2Ljg5OjYxMjM0OmF1dGhfc2hhMV92NDphZXMtMjU2LWNmYjp0bHMxLjJfdGlja2V0X2F1dGg6WTJ4dmRXUm1jbUV1WTI5dC8_b2Jmc3BhcmFtPSZyZW1hcmtzPU1lV1B0dyZncm91cD01THFSNTZ1djVxR0c1cDYy
ssr://MjMuODguMjM2LjkzOjYxMjM0OmF1dGhfc2hhMV92NDphZXMtMjU2LWNmYjp0bHMxLjJfdGlja2V0X2F1dGg6WTJ4dmRXUm1jbUV1WTI5dC8_b2Jmc3BhcmFtPSZyZW1hcmtzPU1lV1B0eTNscElmbmxLZyZncm91cD01THFSNTZ1djVxR0c1cDYy
ssr://MTkyLjE1Ny4yMjguODU6NjEyMzQ6YXV0aF9zaGExX3Y0OmFlcy0yNTYtY2ZiOnRsczEuMl90aWNrZXRfYXV0aDpZMnh2ZFdSbWNtRXVZMjl0Lz9vYmZzcGFyYW09JnJlbWFya3M9TXVXUHR3Jmdyb3VwPTVMcVI1NnV2NXFHRzVwNjI
ssr://MTkyLjE1Ny4yMjguOTA6NjEyMzQ6YXV0aF9zaGExX3Y0OmFlcy0yNTYtY2ZiOnRsczEuMl90aWNrZXRfYXV0aDpZMnh2ZFdSbWNtRXVZMjl0Lz9vYmZzcGFyYW09JnJlbWFya3M9TXVXUHR5M2xwSWZubEtnJmdyb3VwPTVMcVI1NnV2NXFHRzVwNjI
ssr://MjYwNTpmNzAwOjQwOjQwMTo6ODIxMjozOTE4OjYxMjM0OmF1dGhfc2hhMV92NDphZXMtMjU2LWNmYjp0bHMxLjJfdGlja2V0X2F1dGg6WTJ4dmRXUm1jbUV1WTI5dC8_b2Jmc3BhcmFtPSZyZW1hcmtzPU1lV1B0eTFwY0hZMjVMaTcmZ3JvdXA9NUxxUjU2dXY1cUdHNXA2Mg
ssr://MjYwNTpmNzAwOjQwOjQwMTo6ODFkNjo1YWIxOjYxMjM0OmF1dGhfc2hhMV92NDphZXMtMjU2LWNmYjp0bHMxLjJfdGlja2V0X2F1dGg6WTJ4dmRXUm1jbUV1WTI5dC8_b2Jmc3BhcmFtPSZyZW1hcmtzPU1lV1B0eTFwY0hZMjVZbXYmZ3JvdXA9NUxxUjU2dXY1cUdHNXA2Mg
ssr://MjYwNTpmNzAwOjQwOjQwMTo6OTE1YTpiNzA1OjYxMjM0OmF1dGhfc2hhMV92NDphZXMtMjU2LWNmYjp0bHMxLjJfdGlja2V0X2F1dGg6WTJ4dmRXUm1jbUV1WTI5dC8_b2Jmc3BhcmFtPSZyZW1hcmtzPU11V1B0eTFwY0hZMjVMaTcmZ3JvdXA9NUxxUjU2dXY1cUdHNXA2Mg
```
2. 將材料丟進[base64編碼](http://tool.oschina.net/encrypt?type=3)
如下圖所示，將原材料丟進base64編碼會得到右邊亂七八糟的結果
![](/image/ss1.png)
屆時只需將得到的結果存成txt放在網頁上即可
那要如何訂閱呢？只需要輸入`https://xxxxxxxxxx/xxx.txt`


------

本文由 VxRain 創作，採用 知識共享署名4.0 國際許可協議進行許可
本站文章除註明轉載/出處外，均為本站原創或翻譯，轉載前請務必署名
最後編輯時間為: Sep 21, 2017 at 10:19 pm