+++
title = "使用ssh钥匙远程登录Linux服务器"
date = 2023-08-08
+++

## 第1步：生成ssh公钥和私钥
在本地电脑（MacOS 或者 Linux）的命令行中使用：
```bash
ssh-keygen
```
这样就生成了一对私钥和公钥，其默认存储位置为`~/.ssh`。该目录下的`id_rsa`为私钥，`id_rsa.pub`为公钥。此公钥就是用来远程登录的“钥匙”。

## 第2步：将公钥拷贝到远程服务器
参考此教程 [Digital Ocean: How To Configure SSH Key-Based Authentication on a Linux Server](https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server)。几种方法均可行：

1. 自动拷贝：`$ ssh-copy-id username@server_address` 将直接把你的 id_rsa.pub 文件内容拷贝到服务器的 ~/.ssh/authorized_keys 文件中。
2. 半自动拷贝：`cat ~/.ssh/id_rsa.pub | ssh username@server_address "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"`
3. 手动拷贝：在本地打开 id_rsa.pub 拷贝其内容，用 ssh 远程登录后用文本编辑器新建或者编辑 ~/.ssh/auhtorized_keys，将拷贝内容添加进去。

## 第3步：登录
此时在本地打开命令行，远程登录服务器：
```bash
ssh username@server_address
```
现在不需要手动输入密码就能直接登录了！