---
title: urllib添加头信息的两种方法
tags:
  - urllib
categories:
  - Python
abbrlink: 5254b9a
date: 2019-10-01 12:00:00
updated: 2019-10-01 12:00:00
keywords: urllib
description: 记录urllib添加头信息的两种方法
---


## 使用 build_opener

```python
import urllib.request

url = "https://www.baidu.com"
# req = urllib.request.urlopen(url)
headers = ("User-Agent", "Mozilla/5.0 (Windows NT 10.0; WOW64; rv:55.0) Gecko/20100101 Firefox/55.0")
# 使用 build_opener
opener = urllib.request.build_opener()
opener.addheaders = [headers]
# req = opener.open(url)

urllib.request.install_opener(opener)
req = urllib.request.urlopen(url)
```


## 使用 add_header

```python
# 使用 add_header
req = urllib.request.Request(url)
req.add_header("User-Agent", "Mozilla/5.0 (Windows NT 10.0; WOW64; rv:55.0) Gecko/20100101 Firefox/55.0")
res = urllib.request.urlopen(req)

print(res.read())
```
