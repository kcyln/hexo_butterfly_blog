---
title: Requests小技巧和scrapy说明
tags:
  - requests
  - scrapy
categories:
  - Python
abbrlink: fd59dc2b
date: 2019-10-01 12:00:00
updated: 2019-10-01 12:00:00
keywords: requests,scrapy
description: 记录requests几个小技巧和scrapy环境配置
---

## Requests小技巧

* `requests.utils.dict_from_cookiejar` 把cookie对象转化为字典
* 请求SSL证书验证  `requests.get("<https://www.12306.cn/mormhweb/>", verify=False)`
* 配合状态码判断是否请求成功 `assert response.status_code ==200`

## Scrapy

> 爬虫库 python3.6以上

  ```python
  asn1crypto==0.24.0
  attrs==19.1.0
  Automat==0.7.0
  certifi==2019.3.9
  cffi==1.12.3
  constantly==15.1.0
  cryptography==2.6.1
  cssselect==1.0.3
  hyperlink==19.0.0
  idna==2.8
  incremental==17.5.0
  lxml==4.3.3
  parsel==1.5.1
  pyasn1==0.4.5
  pyasn1-modules==0.2.5
  pycparser==2.19
  PyDispatcher==2.0.5
  PyHamcrest==1.9.0
  PyMySQL==0.9.3
  pyOpenSSL==19.0.0
  pywin32==224
  queuelib==1.5.0
  Scrapy==1.6.0
  service-identity==18.1.0
  six==1.12.0
  Twisted==19.2.0
  w3lib==1.20.0
  wincertstore==0.2
  zope.interface==4.6.0
  ```

> 常用命令

  - 全局命令[^1]
    - fetch: 用来显示爬虫爬取过程
    - runspider: 可以实现不依托scrapy的爬虫项目，直接运行一个爬虫文件。
    - settings:
    - shell:
    - startproject:
    - version:
    - view:可以下载某个网页并用浏览器查看。
  - 项目命令
    - bench: 可以测试本地硬件的性能； 运行scrapy bench 时，会创建一个本地服务器并以最大速度爬行
    - check: 爬虫测试比较麻烦，所以在scrapy中使用合同（contract）的方式对爬虫进行测试。
      `scrapy check [爬虫名]`
    - crawl
    - edit: Linux中可以直接打开编辑器编辑爬虫文件
    - genspider: 有多个模板可供选择 参数 -t crawl
    - list: 列出当前可以使用的爬虫文件
    - parse: 获取指定的网址，使用对应的爬虫文件处理和分析



[^1]: 不进入项目目录即可运行

