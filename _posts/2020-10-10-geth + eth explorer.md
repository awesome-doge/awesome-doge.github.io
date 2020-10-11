---
layout: post
title: "geth + eth-netstats"
date: 2020-10-10
tags: [eth,geth,explorer]
categories: [eth,geth]
image: /image/geth.png
description: ""
---


![](/image/geth.png)
* 安裝 geth
* 跑起來
```
geth --rpc --rpcaddr="0.0.0.0" --rpccorsdomain "*"
```

* 下載、安裝 eth-netstats
```
git clone https://github.com/cubedro/eth-netstats
cd eth-netstats
npm install
sudo npm install -g grunt-cli
```

* 下載、安裝  eth-net-intelligence-api
```
git clone https://github.com/cubedro/eth-net-intelligence-api
cd eth-net-intelligence-api
npm install
```

* 安裝 pm2
```
sudo npm install -g pm2
```

## 文件修改
app.json
```
[
  {
    "name"              : "eth-netstate",
    "script"            : "app.js",
    "log_date_format"   : "YYYY-MM-DD HH:mm Z",
    "merge_logs"        : false,
    "watch"             : false,
    "max_restarts"      : 10,
    "exec_interpreter"  : "node",
    "exec_mode"         : "fork_mode",
    "env":
    {
      "WS_SECRET"       : "password",
    }
  }
]

```

app.json
```
[
  {
    "name"              : "eth-net-intelligence-api",
    "script"            : "app.js",
    "log_date_format"   : "YYYY-MM-DD HH:mm Z",
    "merge_logs"        : false,
    "watch"             : false,
    "max_restarts"      : 10,
    "exec_interpreter"  : "node",
    "exec_mode"         : "fork_mode",
    "env":
    {
      "NODE_ENV"        : "production",
      "RPC_HOST"        : "localhost",
      "RPC_PORT"        : "8545",
      "LISTENING_PORT"  : "30303",
      "INSTANCE_NAME"   : "2333.wtf",
      "CONTACT_DETAILS" : "",
      "WS_SERVER"       : "http://localhost:3000",
      "WS_SECRET"       : "password",
      "VERBOSITY"       : 2
    }
  }
]
```

## run
```
cd /home/user/eth-net-intelligence-api
pm2 start app.json
pm2 status
pm2 delete node-app
```

```
cd /home/user/eth-netstats

WS_SECRET=password npm run start

pm2 start app.json
pm2 status
pm2 delete node-app
```