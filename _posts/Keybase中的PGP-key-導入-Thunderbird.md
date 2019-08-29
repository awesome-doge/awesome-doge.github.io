---
title: Keybase中的PGP key 導入 Thunderbird
date: 2019-01-04 18:43:53
tags: [keybase, pgp, thunderbird]
---

前一篇“[Keybase中的PGP](https://chenpowei.github.io/2019/01/04/Keybase中的PGP/)文章中做出簡單的pgp說明，那麼我們應該都有能力得到一個“pgp私鑰” and “pgp公鑰”了。

想要實現一個pgp加密郵件，看了許多文章發現[Thunderbird](https://www.thunderbird.net/zh-TW/)（這是一個很像outlook 的電子郵件代收軟體）是一個不錯的實現pgp加密郵件的地方。

順便一提，Thunderbird 換了新的Logo了呢，原本以為這是一個被放棄更新的project。

![](/image/thunderbird.png)

<!-- more --> 

在Thunderbird 中啟動 pgp ：
1. 安裝[Thunderbird](https://www.thunderbird.net/zh-TW/)
2. 登入原本已經在Keybase綁定的mail
3. 在Thunderbird 中安裝[Enigmail](https://www.enigmail.net/index.php/en/)外掛，Enigmail是一個支持pgp金鑰管理的Thunderbird外掛
![在thunderbird的最上方的工具列多出Enigmail](/image/thunderbird1.png)
4. 打開終端機輸入
```
keybase pgp export -s | gpg --allow-secret-key-import --import -
```
即可把keybase中的 pgp key 導入 電腦中 gpg中
ps. 該指令是參考於“[How to import Keybase private key to use locally with GPG
](https://www.keybits.net/post/import-keybase-private-key/)”
5. 重新開啟Thunderbird後可以發現，原本以Keybase的PGP公鑰加密的郵件都可以順理檢視

![Thunderbird中的Enigmail](/image/thunderbird2.png)