---
title: ubuntu的microk8s真香
date: 2020-08-02 20:18:30
tags:  [microk8s]
---
k8s、docker实在太火了，好像不会这些就要被互联网行业淘汰似的。焦虑，焦虑，平时工作基本上靠gitlab + ansible 基本上就搞定了。为什么不想搞docker , k8s 并不是排斥新技术，实在是我们团队人太少，工作重心更多的投入在开发上面，搞k8s，人力不允许啊。

最近工作上有了些进展，有新同学加入到团队.所以有了一定的时间折腾一下。原来的gitlab用的gitlab官方服务。国内访问效率实在是不敢恭维。所以想自己搭建一套。机会来了，z正好实现一把k8s部署gitlab.

于是安装了ubuntu,看ubuntu文档是，发现microk8s,一套定位开发人员的k8s系统。于是决定尝试一下。基于国内的墙,整个安装过程不算顺利。但是好歹基本上microk8s跑起来了。gitlab也安装完成。但是服务还未配置好，继续折腾吧。

microk8s比较有意思的是直接使用containerd，而不需要运行dockerd。microk8内置了不少插件，只需要简单的microkis enable|disable相关插件即可配置服务。对入门k8s确实比较友好。

至于完整服务等我的gitlab环境完全跑起来之后，再写一篇。
