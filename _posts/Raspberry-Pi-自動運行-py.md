---
title: Raspberry Pi 自動運行 .py
date: 2019-01-08 16:43:45
tags: [raspberry pi, python]
---

方法：

1. 切換到root賬戶　　`sudo su`
2. 修改rc.local文件　　`nano /etc/rc.local`
3. 在exit 0 之前添加執行命令　　`sudo python /xx/xx/xx.py`

![](/image/pi1.png)