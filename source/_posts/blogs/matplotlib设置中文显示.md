---
title: matplotlib设置中文显示
tags:
  - matplotlib
  - Python
categories:
  - 技术杂谈
abbrlink: 695ebb9c
date: 2019-10-01 12:00:00
updated: 2019-10-01 12:00:00
keywords: python,matplotlib
description: matplotlib设置中文显示
---

​matplotlib默认不支持中文字符，因为默认的英文字体无法显示汉字。

* 查看Linux/Mac下面支持的字体

  ```shell
  fc-list 查看支持的字体
  fc-list :lang=zh 查看支持的中文（冒号前面有空格）
  ```


* 修改matplotlib字体

  > 1. 通过matplotlib.rc修改（Windows/Linux），不过测试并没有成功

     ```python
     import matplotlib
     font = {"family": "Microsoft Yahei"}
     matplotlib.rc("font", **font)
     ```


  > 2. 通过matplotlib下的font_manager修改（Windows/Linux/Mac），测试成功

     ```python
     import random
     from matplotlib import font_manager, pyplot
     # fname里面的内容是通过fc-list :lang=zh命令查询到的系统支持的中文字体
     my_font = font_manager.FontProperties(fname=”/usr/share/fonts/truetype/arphic/uming.ttc”)
     a = [random.randint(20,35) for i in range(60)]
     _b = list(range(60))
     _bticks_labels = [“10点%02d分” % i for i in range(60)]
     pyplot.figure(figsize=(30,15))
     # rotation旋转的度数，fontproperties设置字体
     pyplot.xticks(_b[::10], _bticks_labels[::10], rotation=45, fontproperties=my_font)
     pyplot.plot(_b,a)
     ```

