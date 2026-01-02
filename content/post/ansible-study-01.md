---
title: ansible进级之路一
date: 2017-09-13 16:17:01
tags:
---
ansible 做为轻量级运维工具优势还是蛮多的

*   不需要装agnet
*   学习曲线低
*   python实现，模块众多

说了几点优点，来看看它到底有多简单

## 安装

由于ansible由python开发，可以直接通过pip来安装　`pip install ansible` 基本安装就完成

## 配置

经过pip安装的ansible不会默认生成配置文件大家可以到ansible 的github官网找到一份配置[下载][1],把它挪到　/etc/ansible下面及可配置主机列表．在/etc/ansible下面配置一下如机信息格式如下

```bash
        [all]
        192.168.10.33
```

配置公钥访问

## 测试运行命令

```bash
ansible -i /etc/ansible/hosts all -m shell -a "ls -l "
```

-m 指定模块　-a 指定模块的参数

是不是超级简单?

 [1]: https://github.com/ansible/ansible/blob/devel/examples/ansible.cfg