---
layout: post
title: "用docker启动一个mysql容器"
author: "longmeier"
categories: journal
tags: [documentation,sample]
image: spools.jpg
---

### 一、安装docker
 
 yum install -y docker
 
### 二、拉取mysql镜像
 
 docker search mysql  在仓库里面查看mysql镜像版本

 docker pull mysql:5.7  拉取自己想要的镜像

 docker images   查看镜像
    
 * 如果拉取失败，请换成淘宝镜像源
 
### 三、启动mysql 容器
 ``` 
  * 因为mysql数据库是长期存储，必须挂载到本地目录下面。否则mysql容器停止,mysql数据库就丢失了。
  * 先把存放的目录建好
  
  cd /data/mysql
  mkdir -p conf logs data
  
  * 构建mysql容器
  
  docker run --name dmysql -p 3306:3306 -v /data/mysql/conf:/etc/mysql/conf.d -v /data/mysql/logs:/logs -v /data/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD='123456' -d mysql:5.7
  
  --name dmysql   #定义容器的名称dmysql
  
  -p 3306:3306    #服务器的3306端口转发给容器里面的3306端口
  
  MYSQL_ROOT_PASSWORD='123456'  #设置mysql root账号的密码123456
  
  -d mysql:5.7    #指定镜像
     
 ``` 
### 四、查看创建的容器
 ``` 
 
  docker ps -a 查看全部容器
  
  docker exec -it dmysql mysql -uroot -p   连接mysql容器
  
  docker update -restart=always dmysql 容器自动启懂
  
  *查看容器 ip
  
  sudo docker inspect –format ‘{{ .NetworkSettings.IPAddress }}’ dmysql
 ``` 