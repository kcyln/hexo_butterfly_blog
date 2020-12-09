---
title: pip更换国内源
tags:
  - pip
categories:
  - Python
abbrlink: 942da6d9
date: 2020-08-19 00:00:00
updated: 2020-08-19 00:00:00
keywords: pip
description: pip换源，提高下载速度
---

## 介绍

```wiki
1、pip直接安装时速度比较慢，所以使用国内源，可以加速下载模块的速度
2、常用pip源：
	-- 豆瓣：https://pypi.douban.com/simple
	-- 阿里：https://mirrors.aliyun.com/pypi/simple
	-- 清华：https://pypi.tuna.tsinghua.edu.cn/simple
	-- 中国科技大学：https://pypi.mirrors.ustc.edu.cn/simple
3、临时使用以下命令加速安装：
	-- pip install -i https://pypi.douban.com/simple 模块名
```

## 永久配置安装源

### Windows

```wiki
1、资源管理器地址栏输入 %APPDATA% 然后回车，可以直接进入 C:\Users\用户名\AppData\Roaming 目录
2、在此目录下新建 pip 文件夹，并在文件夹中新建 pip.ini 配置文件
3、在 pip.ini 进行配置
```

### MacOS、Linux

```wiki
1、在用户家目录下创建 .pip 隐藏文件夹，如果已经有了可以跳过
	-- mkdir ~/.pip
2、进入 .pip 隐藏文件夹并创建 pip.conf 配置文件
	-- cd ~/.pip && touch pip.conf
3、在 pip.conf 进行配置
```

### 配置文件内容

```ini
[global]
index-url = https://pypi.douban.com/simple
[install]
use-mirrors = true
mirrors = https://pypi.douban.com/simple
trusted-host = pypi.douban.com
```

