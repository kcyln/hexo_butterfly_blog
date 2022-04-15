---
title: Git忽略规则(.gitignore配置）不生效原因和解决
date: 2020-08-07 00:00:00
updated: 2020-08-07 00:00:00
tags:
  - gitignore
categories:
  - 技术杂谈
abbrlink: ede1601b
keywords: git,gitignore
description: 关于.gitignore不生效原因和解决方法
---

**问题**：

​        .gitignore中已经标明忽略的文件目录下的文件，git push的时候还会出现在push的目录中，或者用git status查看状态，想要忽略的文件还是显示被追踪状态。

**回答**：

​        因为在git忽略目录中，新建的文件在git中会有缓存，如果某些文件已经被纳入了版本管理中，就算是在.gitignore中已经声明了忽略路径也是不起作用的，这时候应该先把本地缓存删除，然后再进行git的提交，这样就不会出现忽略的文件了。

**解决方法**：

* git清除本地缓存（改变成未track状态），然后再提交（此方法会删除所有git提交记录，不推荐）

  ```bash
  git rm -r --cached .
  git add .
  git commit -m 'update .gitignore'
  git push -u origin master
  ```

* 在每个clone下来的仓库中手动设置不要检查特定文件的更改情况。

  ```bash
  git update-index --assume-unchanged PATH  # PATH处输入要忽略的文件
  ```

**在使用.gitignore文件后如何删除远程仓库中以前上传的此类文件而保留本地文件**

​        在使用git和github的时候，之前没有写.gitignore文件，就上传了一些没有必要的文件，在添加了.gitignore文件后，就想删除远程仓库中的文件但想保存本地的文件，使用以下命令处理：

```bash
git rm -r –cached directory  # directory 为想要删除的文件夹
git commit -m "delete directory"
git push -u origin master
```

​        这样远程仓库中的文件就被删除了，以后再使用 `git add -A`来添加修改的内容，上传的文件就会受到.gitignore文件的约束。



参考链接： https://www.cnblogs.com/rainbowk/p/10932322.html

