---
title: Keybase中的PGP
date: 2019-01-04 15:41:30
tags: [keybase, pgp]
image: http://chenpowei.github.io/image/keybase5.png
---

keybase 是一個端點加密的通信軟體，在這市面上有許多端點加密的軟體在我們身邊，只是我們完全沒有感覺，或是不知道他的特別。比如說 Facebook messenger and Line 裡面的 悄悄話功能；Telergram 中的 秘密聊天功能；Metrix Riot 的實驗性功能端點加密聊天。執得一提的是，上述中的端點加密功能，都不是預設的，需要比較有隱私潔癖的人才會主動去開啟這些功能。當然也有其他軟體預設去起動的，如史諾登推薦的Signal、Keybase、Whatsapp。

<!-- more --> 

Okay,上面提到了許多端點加密的場景，但是各家通信軟體只是把他們包成了自己的服務，僅僅作為通訊。但"Keybase"把端點加密做成了工具，他自己維護了一個庫，提供，生成pgp私鑰、pgp公鑰、pgp指紋，甚至不只是生成參數，他也可以利用pgp私鑰簽名文件或是信息，透過pgp公鑰去認證文件，又或是透過pgp公鑰加密文件，再透過pgp私鑰解密文件。上述的的功能都在keybase 指令中，如下所示：

```
NAME:
   keybase pgp - Manage keybase PGP keys

USAGE:
   keybase pgp <command> [arguments...]

COMMANDS:
   gen		Generate a new PGP key and write to local secret keychain
   pull		Download the latest PGP keys for people you follow.
   update	Update your public PGP keys on keybase with those exported from the local GPG keyring
   select	Select a key from GnuPG as your own and register the public half with Keybase
   sign		PGP sign a document.
   encrypt	PGP encrypt messages or files for keybase users
   decrypt	PGP decrypt messages or files for keybase users
   verify	PGP verify message or file signatures for keybase users
   export	Export a PGP key from keybase
   import	Import a PGP key into keybase
   drop		Drop Keybase's use of a PGP key
   list		List the active PGP keys in your account.
   purge	Purge all PGP keys from Keybase keyring
   push-private	Export PGP keys from GnuPG keychain, and write them to KBFS.
   pull-private	Export PGP from KBFS and write them to the GnuPG keychain
```

keybase 可能也考慮到指令介面不是很友善，也做了一個網站的版本

1. 加密的頁面（https://keybase.io/encrypt）
![](/image/keybase1.png)
2. 解密的頁面（https://keybase.io/decrypt）
![](/image/keybase2.png)
3. 簽名的頁面（https://keybase.io/sign）
![](/image/keybase3.png)
4. 驗證的頁面（https://keybase.io/verify）
![](/image/keybase4.png)

可以在自己keybase 網頁中找到pgp公鑰：
![](/image/keybase5.png)

keybase 網頁中更詳細的 pgp信息：
![](/image/keybase6.png)

下面的公鑰是我的公鑰

```
 ~ keybase pgp export
-----BEGIN PGP PUBLIC KEY BLOCK-----
Comment: https://keybase.io/download
Version: Keybase Go 2.12.4 (darwin)

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
dy06EEig1CGqj5wKKSwGBpOZBHUxJSumRA==
=J1A8
-----END PGP PUBLIC KEY BLOCK-----
```