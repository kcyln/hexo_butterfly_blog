---
title: ssh连接失败
tags:
  - ssh
categories:
  - Linux
abbrlink: a28edf8d
date: 2019-10-01 12:00:00
---

<!-- more -->

### 问题：ssh: connect to host xx.xxx.xxx.xxx port 22: Connection refused.

1. 检查是否安装ssh服务
    ```
    sudo apt-get install openssh-server
    sudo service ssh start |status
    ```

2. 检查是否开放22端口
    > 查看所有开放端口
    ```
    netstat -aptn | grep 22
    ``` 
    > Ubuntu开放端口方法
    ```
    sudo apt-get update  # 更新源
    sudo apt-get install iptables  # 安装iptables
    sudo iptables -I INPUT -p tcp --dport 8388 -j ACCEPT  # 添加入站规则，开放8388端口
    sudo iptables -save  # 保存
    ```
3. 最终解决方法
    > 查看ssh默认配置文件
    ```
    cat /etc/ssh/sshd_config
    ```
    > 修改配置文件 在Port 28171 下增加 Port 22

    ![](https://cdn.jsdelivr.net/gh/kcyln/ImageHosting@latest/2020/07/28/54dbeb03a6f9e5faea73012741753d6b.png)
    
    > 重启服务     
    ```
    sudo service ssh start
    ```

