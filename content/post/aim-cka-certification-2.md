---
title: CKA备考总结（二）
date: 2020-11-21 16:33:24
tags:
---


本周感觉CKA学习进度有点慢。 本周主要重新部署了microks遇到写问题，折腾花了不少时间。主要是学习了，给应用注入数据，和运行jobs。
在经过这一系列的学习，对k8s的了解也更加深入了一点点，于是趁热大铁把基本概念有过了一遍。

现在的阶段感觉对基本的的操作，基本的的配置都能看懂，但是如果离开文档，还是比较混乱，还没有形成肌肉记忆，这种状态是非常期待的。这些都需要自己的进一步努力了。

下星期目标：就是熟悉集群和网络。时间紧迫要加油了。

这个星期买了台华为云主机，1核心2G，一年89元左右， 挂个blog已经足够了。现在blog采用的hexo静态blog， 所以直接其写了一个docker-compose.yml非常简单，尤其是看了k8s后看docker-compose感觉非常容易理解。nginx的compose配置文件如下：

```yaml
web:
image: nginx
volumes:
- /data/config/nginx/conf.d:/etc/nginx/conf.d
- /data/config/nginx/ssl:/etc/nginx/ssl
- /data/www/npcheng.com:/usr/share/nginx/html
ports:
- "80:80"
- "443:443"
    #  environment:
    #- NGINX_HOST=www.npcheng.com
    #- NGINX_PORT=80
```

现在hexo生成静态文件还是在我的本机完成在推送到线上环境，这还不是很完美，计划用gitlab-ci来处理这一流程，争取本周内解决。
