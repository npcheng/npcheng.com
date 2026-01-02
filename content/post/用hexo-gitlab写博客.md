---
title: 用hexo_gitlab写博客
date: 2018-08-28 21:12:18
tags: [hexo, gitlab]
---

用wordpress写blog好久了，越来越觉得wordpress太重了。而且不太喜欢wordpress自带的编辑器。
最近一直在看gitlab 的CI， hexo对gitlab的支持非常好于是周末时部署了hexo + gitlab
过程很曲折，看最终成功，很开心

长期没有写作，行文特别生硬。甚至有点不知道写写什么，有点尴尬了。不过坚信只要坚持一定能写出像样的文章，不过为了不让文章不太难看，格式还是蛮重要的，所以在google上查看了下有人总结的写作格式.

## 选型

gitlab、github、coding都提供page的功能，github私有仓库貌似有付费，coding没有体验过，gitlab最吸引人的地方是它的gitlab-ci,配置好gitlab-ci之后，只管写博客就ok了，生成静态内容的工作交给gitlab就OK了。

## 部署

### 安装hexo环境

执行以下命令，在本机安装hexo，一共分两步：1. 安装nodejs , 2.安装hexo  我的测试环境是linux,如果是其他操作系统，安装nodejs部分请参考[安装nodejs](https://nodejs.org/en/download/package-manager/)

```bash
yum install gcc-c++ make git -y
curl --silent --location https://rpm.nodesource.com/setup_8.x | sudo bash -
npm install -g hexo-cli
```

### 安装创建本地hexo博客站点

安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。

```bash
hexo init <folder>
cd <folder>
npm install
```

现在本地的hexo就完成了，一共两步：1. 安装hexo 2. 初始化一个本地博客

### 配置gitlab

## 参考文档

* [use hexo setup gitlab page](https://gitlab.com/pages/hexo) 
