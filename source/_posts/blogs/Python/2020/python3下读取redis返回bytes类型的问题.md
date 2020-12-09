---
title: python3下读取redis返回bytes类型的问题
tags:
  - redis
categories:
  - Python
abbrlink: ec1f4cbd
date: 2020-09-23 00:00:00
updated: 2020-09-23 00:00:00
keywords: python3,redis
description: python3下读取redis返回bytes类型而不是字符串解决办法
---

**问题**

使用python连接redis，读取数据时返回的是bytes类型

![](https://cdn.jsdelivr.net/gh/kcyln/ImageHosting@latest/2020/09/23/f3d1bc94d6a48fd3c77426f51333007a.png)

**解决方法**

首先查看连接方法StrictRedis的构造方法

```python
    def __init__(self, host='localhost', port=6379,
                 db=0, password=None, socket_timeout=None,
                 socket_connect_timeout=None,
                 socket_keepalive=None, socket_keepalive_options=None,
                 connection_pool=None, unix_socket_path=None,
                 encoding='utf-8', encoding_errors='strict',
                 charset=None, errors=None,
                 decode_responses=False, retry_on_timeout=False,
                 ssl=False, ssl_keyfile=None, ssl_certfile=None,
                 ssl_cert_reqs=None, ssl_ca_certs=None,
                 max_connections=None):
```

decode_responses=False这个参数决定返回结果是否decode,所以只需要设置连接将其改为true即可

```python
sr = StrictRedis(host='localhost', port=6379,decode_responses=True)
```

