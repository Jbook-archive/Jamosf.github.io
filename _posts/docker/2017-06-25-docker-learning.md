---

layout: post
title: Ubuntu16.04安装Docker的步骤
categories: Docker
description: 搭建的步骤
keywords: ubuntu, docker
---
> 作者：BH

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
 #dockerfie 内容，任一目录新建Dockerfile文件即可
 FROM debian:wheezy  #指定镜像

 RUN apt-get update && apt-get install -y cowsay fortune  #镜像运行的命令

 ENTRYPOINT ["/usr/games/cowsay"]  #指定一个可执行文件，可以是脚本

 #创建镜像命令
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
 #暴露一个端口
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










