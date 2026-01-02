---
title: "在cloudflare 上发布基于 Hugo 的静态博客"
date: 2022-09-03T09:58:14+08:00
draft: flase
---

最近在 cloudflare 上注册了一个域名想着就挂一个静态blog吧，Hugo 当然最好的选择。

用hugo 有短时间了， hugo的发布速度的确飞快，基于markdown的写作方式对于一位放养型blogger 来说hugo 太有好了。

hugo 和cloudflare 的Pages 搭配做静态站点非常方便，简单几步轻松搞定。


### 基本流程

登陆cloudflare 进入控制面板点击右侧的**Pages**, 选择`create a project` 按钮会弹出下拉菜单，选择`connect to git`, Pages 目前支持*github* 和*gitlab* 两个平台。

因为一直使用`gitlab` 所以先择`gitlab` 这时调转到 gitlab.com 完成授权等流程，Pages 页面上会出现项目列表，选择需要发布的项目，点击`begin setup` 按钮。

接着就是配置 *发布选项* 页面,  可以选择 发布的分支，在`Framework preset`选择静态页的框架系统. 我采用的时Hugo 所以选择Hugo 就OK了。后续的指令系统会制动补全。

点击 `Save and Deploy ` 发现系统有报错。

### 错误分析

很不幸发现了报错信息，一般情况下时发布系统环境变量引起的。比如选错了hugo 的版本时最多的问题。

比如遇到的是
` shortcodes/admonition.html:4: function "merge" not defined`

在这也不要慌， 点击`Environment variables (advanced)` 页面会显示一个`Add variable` 的按钮点击它，加上一个环境变量`HUGO_VERSION`, 这个环境变量与你的本地hugo程序版本一致，就OK。
再次发布， 完美程序发布完成， 下一步配置好自己的域名把自己的域名cname到Pages 的域名上就OK了。

开心的是，https都集成了，省力省心。


