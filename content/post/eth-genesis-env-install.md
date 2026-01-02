---
title: 以太坊blockchain测试环境搭建
date: 2018-03-20 16:14:02
tags:
---

## 安装以太坊客户端

```bash
wget "https://gethstore.blob.core.windows.net/builds/geth-linux-amd64-1.8.2-b8b9f7f4.tar.gz" && tar xvfz geth-linux-amd64-1.8.2-b8b9f7f4.tar.gz && mv geth-linux-amd64-1.8.2-b8b9f7f4.tar.gz /data/geth
```

## 创建挖矿账号

`geth account new --datadir <path-to-data-directory>` path-to-data-directory 可以自定义目录 我这里是/data1/geth/.ethereumdata

```bash
./geth account new --datadir /data1/geth/.ethereumdata
INFO [03-20|14:47:42] Maximum peer count                       ETH=25 LES=0 total=25
Your new account is locked with a password. Please give a password. Do not forget this password.
Passphrase: 
Repeat passphrase: 
Address: {bfb5cf2c07fe93d005d2e70e8a782b30a52ed3fb} 
```

## 创建创世块

```bash
./geth --datadir /data1/geth/.ethereumdata init genesis.json
```

## 运行geth

```bash
nohup ./geth --mine --rpc  --rpcapi "eth,net,web3" --rpcaddr 0.0.0.0 --rpccorsdomain "*" --datadir /data1/geth/.ethereumdata >> ./geth.log
```

## 连接geth console

```bash
./geth attach ipc:/root/.ethereum/geth.ipc
```
