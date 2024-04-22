---
title: Hyperledger Fabric trace Project
date: 2024-04-21 13:28:27
tags: 项目搭建
---
# 快速项目搭建运行

1.打开腾讯云服务器
2.启动区块链网路服务

>> ./start.sh  *开始*

>> ./stop.sh  *停止*

**如果报错**

## 执行清理所有的容器指令：

>> docker rm -f $(docker ps -aq)

3.启动前后端服务
进入fabric-trace/application/backend

>> go run main.go

进入fabric-trace/application/web

>> npm install  

>> npm run dev 

[项目原地址](https://github.com/TrueTechLabs/fabric-trace)