---
title: Thunderbird 字體太小筆記 (for mac)
date: 2018-01-30 05:33:06
tags: [thunderbird, mac]
---

因為mac os 中，要對mail.app設置『獨自』的proxy代理好像有點困難，所以只好跳槽去Thunderbird，但一次裝Thunderbird 發現有些版面字體版面實在是太小了眼睛看不到，而且還沒有地方可以設定，於是爬了一下文。

<!-- more --> 

需要到 /Users/使用者名稱/Library/Thunderbird/Profiles/一串亂碼.default/chrome 底下（chrome 資料夾一開始是不存在的，請自行創建）創建一個名為userChrome.css的檔案進行編輯。貼上之後 可以條條裡面的相關參數，存擋之後，重啟 Thunderbird就會看到效果了。

```
/* set default namespace to XUL */
@namespace
url(“http://www.mozilla.org/keymaster/gatekeeper/there.is.only.xul");
/* Set Font Size In Folder Pane */
#folderTree >treechildren::-moz-tree-cell-text {
 font-size: 11pt !important; }
/* Set Font Size In Thread Pane */
#threadTree >treechildren::-moz-tree-cell-text {
 font-size: 11pt !important; }
/* Set Height For Cells In Folder Pane */
#folderTree >treechildren::-moz-tree-row {
 height: 22x !important; }
/* Set Height For Cells In Thread Pane */
#threadTree >treechildren::-moz-tree-row {
 height: 22px !important; }
/* Global UI font */
* { font-size: 11pt !important;
 font-family: Verdana !important;
}
```