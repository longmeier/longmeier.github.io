---
layout: post
title: "sentry收集项目bug钉钉通知"
author: "Paul Le"
categories: journal
tags: [documentation,sample]
image: cards.jpg
---

### 一、docker部署sentry
 ``` 
    git clone https://github.com/getsentry/onpremise.git  获取sentry安装包 解压
    *操作流程
    1. mkdir -p data/{sentry,postgres}
    2. docker-compose build
    3. docker-compose run --rm web config generate-secret-key
    4. docker-compose run --rm web upgrade
    5. docker-compose up -d
    6. localhost:9000
  ``` 
### 二、sentry 配置钉钉
 ``` 
    *在钉钉群里面建一个自定义机器人（群主才能建），把access_token 复制出来
    1. git clone https://github.com/gzhappysky/sentry-dingtalk.git
       pip install sentry-dingtalk
    2. requirements.txt新增包  sentry-dingding~=0.0.1
    3. 重新build 重启
       docker–compose build
       docker–compose up –d
 ``` 
### 三、sentry后台启用钉钉通知插件
 ``` 
     * 进入sentry 项目里面找到所有插件 DingDing 启用插件、把access_token 的values 保存进去就行了。
 ``` 