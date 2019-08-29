---
title: bitcoin.cz
date: 2014-08-29 18:10:54
tags: [blogger, miner, pool, bitcoin]
categories: Blogger
---

https://mining.bitcoin.cz/accounts/profile/

1. 在您電腦安裝比特幣礦工

大多數的CPU/GPU礦工都能支持集體發掘：

Kiv的GUI礦工（Windows,建議給初學者) (說明)
ckolivas's CGMINER (GPU/FPGA, recommended for experts) (說明)
m0mchil的GPU礦工 (說明)

<!-- more --> 

2. 使用bitcoin.cz帳戶來註冊

註冊
確認電郵地址（可能用於故障排除）
Login to application
請輸入您的錢包地址 MtGox 或 Intersango
Register your workers. You can use one worker account for all your miners, but I recommend to use separate account for every miner for easier troubleshooting.

3. 進行礦工

Run y​​our own GPU/FPGA/ASIC miner with the worker credentials you gave earlier, and connect it to following URL:
http://api.bitcoin.cz:8332
(Main pool URL)

或
stratum.bitcoin.cz:3333
(If you have Stratum-compatible miner)