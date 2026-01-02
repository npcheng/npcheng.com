---
title: windows10配置GOROOT GOPATH环境变量
date: 2018-09-03 11:30:47
tags: [golang]
---

在windows环境下写golang, 开发环境：vs code, 写了段helloworld， vscode提示`expected 'package', found 'EOF'`, google之后判断是环境变量的事情。 

golang有三个环境变量：path, GOROOT, GOPATH ,分别是啥意思？刚开始写golang感觉有点懵，先打开golang的[官方手册](https://github.com/golang/go/wiki/SettingGOPATH)看看，

PATH: 是GO的安装目录下的bin目录

GOROOT: 即GO的安装目录

GOPATH: 我的理解就是我的工作目录，即项目文件夹

如果使用vscode 最好吧go代码放在工作目录下的src目录下，否则就会报`expected 'package', found 'EOF'`

配置完成可以开心的学习golang, 刚开始使用，可能有坑，文档会持续更细，让大家少踩坑

## 参考文档

* [golang安装文档](https://golang.org/doc/install)
* [聊聊GOPATH、GOROOT](https://studygolang.com/articles/10194)
* [Golang学习之GOROOT、PATH、GOPATH及go get](https://my.oschina.net/yearnfar/blog/187266)
