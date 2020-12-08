---
title: 部署awesome时报错
tags:
  - supervisor
categories:
  - Linux
abbrlink: cb42f876
date: 2019-10-01 12:00:00
---

<!-- more -->

```
[program:awesome]
command = /home/kcyln/srv/awesome/www/app.py
directory = /home/kcyln/srv/awesome/www
user = www-data
startsecs = 3

redirect_stderr = true
stdout_logfile_maxbytes = 50MB
stdout_logfile_backups = 10
stdout_logfile = /home/kcyln/srv/awesome/log/app.log
```

​    如上设置, 运行提示 is not executable

​    修改 `command = python3 /home/kcyln/srv/awesome/www/app.py`

​    报错  Exited too quickly (process log may have details)

​    检查日志发现 提示     ModuleNotFoundError: No module named 'markdown'

​    然而我已经使用 `pip install markdown` 安装成功了

​    尝试 使用虚拟环境，设置 

```
command = /bin/bash -c 'source "0" && exec "@"' /home/kcyln/.virtualenvs/awesome_env/bin/activate ; python3 /home/kcyln/srv/awesome/www/app.py
```

​    仍然失败

​    最后使用 `sudo apt-get install markdown && sudo apt-get install python3-markdown`

​    成功