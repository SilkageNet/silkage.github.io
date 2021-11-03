+++
banner = ""
categories = ["学习笔记"]
date = "2019-10-11T15:30:00+08:00"
description = ""
images = []
menu = ""
tags = ["ssh"]
title = "SSH如何免密登录"
+++

以前使用ssh登录服务器，每次都需要输入密码，比较反锁，特别是随机生成的密码还需要复制粘贴。所以了解了下ssh的免密登录的方法，用起来很方便，对管理很多服务也比较简便。

<!--more-->

- 生成 `rsa` 密钥对文件, 文件名 `ali_server`

```bash
ssh-keygen -t rsa
```

- 在 `~/.ssh/config` 中添加host信息

```nginx
# 服务器备注
Host ali_server # 对服务器取个别名方便登录
HostName 110.110.110.110 # 服务器地址
Port 22 # 服务器端口
User root # 登录用户
IdentityFile ~/.ssh/server/ali_server # 密钥文件路径
```

- 将公钥 `*.pub` 文件写入服务器

```bash
cat ali_server.pub | ssh -p 22 root@110.110.110.110 'cat >> ~/.ssh/authorized_keys'
```

- 配置成功, 登录服务器

```bash
ssh ali_server
```

