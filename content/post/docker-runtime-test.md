---
title: docker学习二:docker 运行服务测试
date: 2016-11-4 16:02:01
tags:
---

## docker 运行服务测试

测试例子django采用hub.docker.com中官方的镜像:<https://hub.docker.com/_/django/>

运行命令：

```bash
docker run -it -v $PWD:/usr/src/app -w -w /usr/src/app django django-admin.py startproject mysite
```

用途：下载镜像,运行容器并创建django项目，把当前目录挂载到/usr/src/app目录下，指定工作目录为/usr/src/app

启动django服务：

```bash
docker run  -v "$PWD":/usr/src/app -w /usr/src/app -p 8000:8000 -d django bash -c "python manage.py runserver 0.0.0.0:8099"
```

运行mysql:

```bash
docker run -e MYSQL_ROOT_PASSWORD=xxxx -d mysql/mysql-server
```

查看结果：

```bash
[root@localhost ~]# docker ps -a`CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES\``db2e268ba122 mysql/mysql-server "/entrypoint.sh mysql" 8 seconds ago Up 7 seconds 3306/tcp, 33060/tcp hungry_gates
```

django容器与mysql容器保持通信

```bash
docker run -it -d -p 8099:8099 --link hungry_gates:db -v $PWD:/usr/src/app -w /usr/src/app/mysite django   python manage.py runserver 0.0.0.0:8099
```

进入容器内 django 创建superadmin, 修改django的数据库连接方式，host选择db
