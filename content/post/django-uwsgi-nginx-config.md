---
title: 配置django_uwsgi_nginx
date: 2018-09-12 16:48:41
tags: [django,uwsgi, nginx]
---

django默默的更新到了2.1了，我们在用1.11做开发，没别的，我们的开发环境还是python2.7,django 1.11应该是最后一个支持python2.7的版本了。

django + uwsgi + nginx 应该是一个标配了， django 做应用，uwsgi 做wsgi网关， nginx做webserver, 在负载不大的情况下nginx在一层可以不要。这里头可能uwsgi配置会相对麻烦已写，所以记录下来

## 创建django测试程序

```bash
mkdir /data/www/projectdir
pip install django

```

## uwsgi配置

### 安装uwsgi

```bash
pip install uwsgi
```

### 配置uwsgi

创建/etc/uwsgi.d,编辑/etc/uwsgi.d/app.ini

```bash
mkdir -p /etc/uwsgi.d

cat > /etc/uwsgi.d/app.ini <<EOF
[uwsgi]
http = 0.0.0.0:80 # 如果前端加nginx 请把http换成socket
chdir = /data/www/projectdir/
module=project.wsgi:application
# module=django.core.handlers.wsgi:WSGIHandler() 
env =  DJANGO_SETTINGS_MODULE=project.settings
master = true
process = 10
thread= 2
daemonize = /var/log/uwsgi/app.log
pidfile=/var/log/uwsgi/app.pid
vacuum=True
EOF
```

指令解读：

- *module*  使用的wsgi模块
- *env*  设置环境变量 DJANGO_SETTINGS_MODULE
- *chdir* django项目所在目录
- *daemonize* 设置日志文件

上述指令没有指定user, 默认user是root, 请谨慎配置user

### 运行和停止uwsgi

```bash
## 运行uwsg
uwsgi --ini /etc/uwsgi.d/app.ini
## 停止uwsg ,
uwsgi --stop /var/log/uwsgi/app.pid
```

## 配置nginx

```bash
yum install -y nginx
mkdir - /etc/nginx/site-enable.d
cat > /etc/nginx/site-enable.d/vtc123.com <<EOF
server {
    # the port your site will be served on
    listen      80;
    # the domain name it will serve for
    server_name www.vtc123.com vtc123.com; # substitute your machine's IP address or FQDN
    charset     utf-8;

    # max upload size
    client_max_body_size 75M;   # adjust to taste

    location /static {
        alias /data/project/vtc123/static; # your Django project's static files - amend as required
    }

    # Finally, send all non-media requests to the Django server.
    location / {
        uwsgi_pass  vtc123;
        include uwsgi_params;
    }
}
EOF

cat >/etc/nginx/conf.d/vtc123.conf <<EOF
    upstream vtc123 {
    server 127.0.0.1:8088;
}
EOF
```

`/etc/nginx/site-enable.d/*.conf` 插入到nginx.conf配置文件中让site-enable.d目录下的配置文件生效

## 启动服务

```bash
#nginx
systemctl enable nginx&&systemctl start nginx
usgi --ini /etc/uwsgi.d/app.ini  #运行uwsgi
uwsgi --stop /var/log/uwsgi/app.pid #停止uwsgi 
```

## 参考文档

- [howto_deploy_django_uwsgi](https://docs.djangoproject.com/en/1.11/howto/deployment/wsgi/uwsgi/)
- [uwsgi_docs](https://uwsgi-docs.readthedocs.io/en/latest/)
- [理解wsgi& uwsgi](https://www.jianshu.com/p/679dee0a4193)
