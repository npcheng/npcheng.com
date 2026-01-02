---
title: "helm3快速入门"
date: 2022-03-23T11:20:40+08:00
draft: false
tags: ["kubernetes"]
---

kubernets 在希腊语指的是舵手，这个在容器世界里头很形象， kubernetes 调度着各种资源。

而helm 又是什么呢？helm英文值得是舵， 哈哈，正所谓秤不离砣， 砣不离秤。 同样的舵手离不开舵。

想必大家都有使用rpm、apt、pip、docker等包管理系统安装过包。其实helm也可以这样认为就是一套kuberntes的包管理系统。

可能有人会问， docker 可以通过dockerfile 来管理docker包， 为什么还要再制造一个helm出来？

docker 的包管理系统和helm的包管理系统其实是应用在不同层面。

dockerfile 只是负责制作image ， docker pull/push 负责下载/发布images. 它的作用层面在container层。

helm 不负责制作管理images， 它负责的对象是kubernetes的所有对象，除了Node节点不归它管理，这些对象有哪些呢？

- Namespace
- NetworkPolicy
- ResourceQuota
- LimitRange
- PodSecurityPolicy
- PodDisruptionBudget
- ServiceAccount
- Secret
- SecretList
- ConfigMap
- StorageClass
- PersistentVolume
- PersistentVolumeClaim
- CustomResourceDefinition
- ClusterRole
- ClusterRoleList
- ClusterRoleBinding
- ClusterRoleBindingList
- Role
- RoleList
- RoleBinding
- RoleBindingList
- Service
- DaemonSet
- Pod
- ReplicationController
- ReplicaSet
- Deployment
- HorizontalPodAutoscaler
- StatefulSet
- Job
- CronJob
- Ingress
- APIService

helm 其实可以简单理解就是一个批处理脚本， 根据资源列表按照顺序依次执行相关操作， 说通俗点检就是把手工配置kubernetes的工作交给helm这个脚本来执行。

既然helm这么厉害， 不掌握确实可惜， 把helm知识点梳理一下，也是极好的。

好了这篇文章先水到这里,未完待续。这篇文章会持续更新。
