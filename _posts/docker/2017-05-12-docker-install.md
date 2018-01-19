---

layout: post
title: Ubuntu16.04安装Docker的步骤
categories: Docker
description: 搭建的步骤
keywords: ubuntu, docker
---
> 作者：BH


Docker是一种容器，但它是轻量级的。目前在中国，已经有许多Docker使用者，也建立了相应的中文社区。Docker组件包括：Docker客户端和服务器、Docker镜像、Registry和Docker容器。
那么，下面记录一下在linux中安装Docker的步骤。

### 检查内核版本

在linux中使用命令即可：
```
$ name －a 
```
### 检查Device Mapper

```
$ sudo grep device-mapper /proc/devices

```
###  添加Docker的APT仓库
```
$ sudo sh -c "echo deb https://get.docker.io/ubuntu docker main> /etc/apt/sources.list.d /docker.list"

```
###	添加Docker仓库的GPG密钥
```
$ curl -s https://get.docker.io/gpg | sudo apt-get add -
```
在这一步安装的过程中很容易碰到提示：gpg: no valid OpenPGP data found. 这是因为电脑不能访问外网导致的，向终端输入以下代码：
```
$ gpg --keyserver pgpkeys.mit.edu --recv-key D8576A8BA88D21E9

$ gpg -a --export  D8576A8BA88D21E9 | sudo apt-key add -
```
结果会提示ok，但是ok不一定代表成功。D8576A8BA88D21E9这一串数字换成自己的公钥（public key）。先继续下一步。

### 更新APT源
```
$ sudo apt-get update
```
### 安装Docker软件包
```
$ sudo apt-get install lxc-docker
```
### 检查Docker是否已经成功安装
```
$ sudo docker info
```

### UFW文件更改
```
$ vi /etc/default/ufw
$ DEFAULT_FORWARD_POLICY="ACCEPT"
$ sudo ufw reload     
```
### 绑定到网络接口
```
$ sudo /usr/bin/docker -d -H tcp://0.0.0.0:2375
```

### 增加环境变量
```
export DOCKER_HOST="tcp://0.0.0.0:2375"
```

### 检查是否运行
```
$ sudo status docker
```
 这时系统又出现提示：status: Unable to connect to Upstart: Failed to connect to socket /com/ubuntu/upstart: Connection refused。可以通过修改upstart和system的默认启动方式解决。也可以在不修改的情况下通过下面的命令查看：
```
$ service docker status
```