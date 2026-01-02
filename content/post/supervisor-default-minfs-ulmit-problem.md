---
title: supervisor默认minfs问题
date: 2017-02-7 16:10:01
tags: [ulimit, linux]
---
昨天有爬虫同事说:我的爬虫并发量一大,就报大量的错误lookup live.xxxxxx.com on 10.143.22.118:53: no such host .从现象上看是dns未解析所访问的域名.我们的使用的是阿里云的ecs内部dns,初步怀疑是阿里云对请求数有限制,和阿里沟通阿里云说没有限制.

我来爬虫组说如果手动运行爬虫程序就没有报错了.这时候想起来了,我们的爬虫程序是用supervisor来管理的,在/etc/supervisord.conf中文件描述符是1024

```bash
minfds=1024                 ; (min. avail startup file descriptors;default 1024)
```

查看supervisord的主进程的limits信息如下

```bash
cat /proc/6608/limits 
Max open files            1024                4096                files 
```

修改supervisord的minfds=65535服务恢复正常