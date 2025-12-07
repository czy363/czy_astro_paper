---
author: 轩邈
pubDatetime: 2025-11-15T19:57:19+08:00
modDatetime: 2025-11-15T19:57:19+08:00
title: 搭建chronoframes画廊详细教程
featured: false
draft: false
tags:
  - 博客搭建
description: 搭建chronoframes画廊教程
---

### 1. 安装docker

#### （1）远程登录服务器，查看阿里云服务器系统

```bash
admin@iZuf6fl1lkbj829ezx5i7qZ:~$ cat /etc/os-release | grep -E '^ID='
ID=ubuntu
```

#### （2）添加Docker软件包源 + 安装Docker社区版本

```bash
#更新包管理工具
sudo apt-get update
#添加Docker软件包源
sudo apt-get -y install apt-transport-https ca-certificates curl software-properties-common
sudo curl -fsSL http://mirrors.cloud.aliyuncs.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository -y "deb [arch=$(dpkg --print-architecture)] http://mirrors.cloud.aliyuncs.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
#安装Docker社区版本，容器运行时containerd.io，以及Docker构建和Compose插件
sudo apt-get -y install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

#### （3）启动Docker并设置开机自启

```bash
#启动Docker
sudo systemctl start docker
#设置Docker守护进程在系统启动时自动启动
sudo systemctl enable docker
```

#### （4）配置镜像源

```bash
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://rxoe304z.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

#### （5）验证docker是否安装成功

###### 查看版本

```bash
admin@iZuf6fl1lkbj829ezx5i7qZ:~$ docker --version
Docker version 28.1.1, build 4eba377
```

###### 检查 Docker 服务状态

```bash
admin@iZuf6fl1lkbj829ezx5i7qZ:~$ sudo systemctl status docker.service
● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: active (running) since Fri 2025-11-28 21:32:16 CST; 21min ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 1995867 (dockerd)
      Tasks: 11
     Memory: 25.7M
     CGroup: /system.slice/docker.service
             └─1995867 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
```



### 2.安装docker-compose

```bash
admin@iZuf6fl1lkbj829ezx5i7qZ:~$ sudo apt-get -y install docker-compose-plugin
Reading package lists... Done
Building dependency tree       
Reading state information... Done
docker-compose-plugin is already the newest version (2.35.1-1~ubuntu.20.04~focal).
0 upgraded, 0 newly installed, 0 to remove and 165 not upgraded.
```



### 3. 拉取chronoframes docker镜像

```bash
# 从 GHCR 拉取（推荐）
docker pull ghcr.io/hoshinosuzumi/chronoframe:latest
```





##### 📚参考链接：

https://swasnext.console.aliyun.com/servers/cn-shanghai

https://mp.weixin.qq.com/s/C2udgzu3ixkzHYMpkxqbDA

https://cr.console.aliyun.com/cn-shanghai/instances/mirrors

https://docs.world-creator.com/zh/can-kao/terrain/shape-layers/maptiler

https://cloud.maptiler.com/account/credentials/
