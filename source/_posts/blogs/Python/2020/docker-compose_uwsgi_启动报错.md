---
title: docker-compose启动后其中的web容器立刻停止
tags:
  - docker
  - docker-compose
  - django
  - uwsgi
categories:
  - Python
abbrlink: 9fd46b0b
date: 2020-09-20 00:00:00
updated: 2020-09-20 00:00:00
keywords: docker-compose
description: 启动uwsgi时由于设置了守护进程导致容器直接停止
---


**背景**

​        使用docker-compose+django+uwsgi+nginx部署网站时，刚一启动web容器就停止了，也导致nginx启动失败。

**原因**

​        uwsgi.ini配置中添加了 daemonize=uwsgi.log 导致uwsgi程序日志输出到指定的文件， 进程会在后台运行，docker前台没有程序运行，所以停止了。

​        Docker容器同时只能管理一个进程，如果这个进程退出那么容器也就退出了，但这不表示容器只能运行一个进程(其他进程可在后台运行)，但是要使容器不退出必须有一个前台执行的进程。

**解决方法**

​        将daemonize=uwsgi.log注释或者删除即可。