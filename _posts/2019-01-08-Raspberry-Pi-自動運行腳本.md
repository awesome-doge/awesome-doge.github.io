---
layout: post
title: Raspberry Pi 自動運行腳本
date: 2019-01-08 16:43:45
tags: [raspberry pi, python]
---

方法：

1. 切換到root賬戶　　`sudo su`
2. 修改rc.local文件　　`nano /etc/rc.local`
3. 在exit 0 之前添加執行命令　　`指令內容`

![](/image/pi1.png)
