---

layout: post
title: Ubuntu16.04安装Docker的步骤
categories: Docker
description: 搭建的步骤
keywords: ubuntu, docker
---
> 作者：Jamosf

<h1 style="text-align:center">一、docker安装</h1>

Docker是一种容器，但它是轻量级的。目前在中国，已经有许多Docker使用者，也建立了相应的中文社区。Docker组件包括：Docker客户端和服务器、Docker镜像、Registry和Docker容器。
那么，下面记录一下在linux中安装Docker的步骤。

1. 检查内核版本

在linux中使用命令即可：
```
$ name －a 
```
2. 检查Device Mapper

```
$ sudo grep device-mapper /proc/devices
```
3. 添加Docker的APT仓库

```
$ sudo sh -c "echo deb https://get.docker.io/ubuntu docker main> /etc/apt/sources.list.d /docker.list"
```
4. 添加Docker仓库的GPG密钥

```
$ curl -s https://get.docker.io/gpg | sudo apt-get add -
```
在这一步安装的过程中很容易碰到提示：gpg: no valid OpenPGP data found. 这是因为电脑不能访问外网导致的，向终端输入以下代码：
```
$ gpg --keyserver pgpkeys.mit.edu --recv-key D8576A8BA88D21E9
$ gpg -a --export  D8576A8BA88D21E9 | sudo apt-key add -
```
结果会提示ok，但是ok不一定代表成功。D8576A8BA88D21E9这一串数字换成自己的公钥（public key）。先继续下一步。

5. 更新APT源

```
$ sudo apt-get update
```
6. 安装Docker软件包

```
$ sudo apt-get install lxc-docker
```
7. 检查Docker是否已经成功安装

```
$ sudo docker info
```

8. UFW文件更改

```
$ vi /etc/default/ufw
$ DEFAULT_FORWARD_POLICY="ACCEPT"
$ sudo ufw reload     
```
9. 绑定到网络接口

```
$ sudo /usr/bin/docker -d -H tcp://0.0.0.0:2375
```

10. 增加环境变量

```
export DOCKER_HOST="tcp://0.0.0.0:2375"
```

11. 检查是否运行

```
$ sudo status docker
```
 这时系统又出现提示：status: Unable to connect to Upstart: Failed to connect to socket /com/ubuntu/upstart: Connection refused。可以通过修改upstart和system的默认启动方式解决。也可以在不修改的情况下通过下面的命令查看：
```
$ service docker status
```

> 更新：现在直接使用apt-get install 命令就可以安装了，无需上面的步骤。

<h1 style="text-align:center">三、docker常用命令</h1>

1. 安装mac的boot2docker工具：可以使用brew install boot2docker或者下载boot2docker的客户端安装程序，但前者需要自己安装virtualbox虚拟机，后者安装包内带virtualbox
2. 运行简单的docker程序

```
 docker run -it cowsay /bin/bash
```

3. 把容器转换成镜像：

```
 docker commit cowsay test/cowsayimage
```

4. 运行本地打包的镜像

```
 docker run test/cowsayimage bash
```

5. 利用dockerfile构建对象

```
 dockerfie 内容，任一目录新建Dockerfile文件即可
 FROM debian:wheezy  #指定镜像
 RUN apt-get update && apt-get install -y cowsay fortune  #镜像运行的命令
 ENTRYPOINT ["/usr/games/cowsay"]  #指定一个可执行文件，可以是脚本
 创建镜像命令
 docker build -t jiamosi/cowsay-dockfile .
```

6. 发布镜像

```
 docker push jiamosi/cowsaycowsay-dockfile  # 镜像的名称前面一定是dockerhub用户名
```

7. 删除容器

```
 docker rm containerid
```

8. 删除已经退出的容器

```
 docker rm -v $(docker ps -aq -f status=exited)
```

9. docker使用link连接两个容器

```
 docker run --rm -it --link myredis:redis redis /bin/bash #将我的redis与最新的redis连接起来，并且启动新的redis，使用redis-cli看看
 redis-cli -h redis -p 6379 # redis是myredis在新redis容器中的/etc/hosts映射myredis的ip地址的主机名称
```

10. 容器与世界互联

```
 暴露一个端口
 docker run -d -p 8000:80 nginx  # 将主机的8000端口转发给容器的80端口
 或者
 docker run -d -p nginx # 自动选择一个主机上未使用的端口
 docker port $(docker run -d -p nginx) 80  #可以查看容器的80端口对应的主机端口
```

11. 下载一个mysql的镜像，并运行起来。

```
 docker run --name mysqlroot -e MYSQL_ROOT_PASSWORD=cloud -d mysql:latest
 docker exec -it mysqlroot bash
 mysql -u root -pcloud
```