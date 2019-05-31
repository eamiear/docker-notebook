# 安装 NGINX

```bash

[root@server-test-212 ~]# docker run -d --name nginx -v /data/nginx/web:/usr/share/nginx/html  -p 80:80 nginx:stable-alpine
3d6a673c9adbd232f40bace7c2abe20e9143cbfedb632ad46b1df88d60e47a1a

```

查看进程

```bash

[root@server-test-212 ~]# docker ps
CONTAINER ID        IMAGE                     COMMAND                  CREATED             STATUS                  PORTS                                              NAMES
3d6a673c9adb        nginx:stable-alpine       "nginx -g 'daemon of…"   3 seconds ago       Up 1 second             0.0.0.0:80->80/tcp                                 nginx


```