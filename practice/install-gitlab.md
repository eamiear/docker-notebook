# 使用 docker 安装 gitlab

### 配置执行

```bash
[root@server-test-212 srv]# docker run --detach --hostname gitlab.on-bright.com --publish 8000:80  --name gitlab --restart always --volume /srv/gitlab/config:/etc/gitlab --volume /srv/gitlab/logs:/var/log/gitlab --volume /srv/gitlab/data:/var/opt/gitlab --env GITLAB_OMNIBUS_CONFIG="external_url 'http://192.168.200.212';"  gitlab/gitlab-ce:latest

```

执行结果
```
ce:latest
Unable to find image 'gitlab/gitlab-ce:latest' locally
latest: Pulling from gitlab/gitlab-ce
9ff7e2e5f967: Pull complete 
59856638ac9f: Pull complete 
6f317d6d954b: Pull complete 
a9dde5e2a643: Pull complete 
b3c5ef1d56d6: Pull complete 
dcf09f02c776: Pull complete 
6aa7102acdd8: Pull complete 
7edf5e8320ad: Pull complete 
a8dcef22ce7c: Pull complete 
411efb930539: Pull complete 
Digest: sha256:51bf76a9018347ba525948902e82f30451b90a06d22e4c52ce5533b464e3864d

```

### 登录修改密码

在浏览中输入 `http://192.168.200.212:8000`，提示修改密码，修改密码后重新登录。

默认账户 root

### 查看gitlab运行日志

```bash
docker logs gitlab

docker logs -f gitlab

```

### 进入容器

```bash
docker exec -it gitlab /bin/bash

```

### 宿主机器与容器间的文件传递

```shell
Usage:  docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-
	docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH
```

```bash
# 宿主机器文件复制到容器
docker cp gitlab-11-10-statble-zh gitlab:/opt/
```

### 参考

https://docs.gitlab.com/omnibus/docker/

### 汉化

#### 查看gitlab版本

```bash
root@gitlab:/opt# cat /opt/gitlab/embedded/service/gitlab-rails/VERSION
11.11.0

```

#### 下载汉化包
https://gitlab.com/xhang/gitlab

git@gitlab.com:xhang/gitlab.git
https://gitlab.com/xhang/gitlab/-/archive/11-10-stable-zh/gitlab-11-10-stable-zh.tar

#### 备份gitlab文件

 /opt/gitlab/embedded/service/gitlab-rails/

#### 替换覆盖

```bash
root@gitlab:/opt# cp -rf gitlab-11-10-stable-zh/* /opt/gitlab/embedded/service/gitlab-rails/
cp: cannot overwrite non-directory '/opt/gitlab/embedded/service/gitlab-rails/log' with directory 'gitlab-11-10-stable-zh/log'
cp: cannot overwrite non-directory '/opt/gitlab/embedded/service/gitlab-rails/tmp' with directory 'gitlab-11-10-stable-zh/tmp'
```

```bash
# 重新配置
root@gitlab:/opt# gitlab-ctl reconfigure

```

```bash
# 重启gitlab
root@gitlab:/opt# gitlab-ctl restart

```
