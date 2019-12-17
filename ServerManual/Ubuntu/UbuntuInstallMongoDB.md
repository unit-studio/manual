# Ubuntu 安装 MongoDB

## 通过 tgz 包进行安装

```shell
# 切换到指定目录
$ cd /usr/local/packages

# 下载安装包
$ wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-ubuntu1804-4.2.1.tgz

# 解压
$ tar -zxvf mongodb-linux-x86_64-ubuntu1804-4.2.1.tgz

# 将 MongoDB 的可执行文件添加到 PATH 路径中
# <mongodb-install-path> 为你 MongoDB 的安装路径。如本文的 /usr/local/mongodb 。
$ export PATH=<mongodb-install-path>/bin:$PATH
```

## 创建 MongoDB 目录

> 注意：/data/db 是 MongoDB 默认的启动的数据库路径(--dbpath)。

```shell
$ mkdir -p /data/db
```

## 启动 mongodb 服务

```shell
$ ./mongod
```

## 使用 mongoShell 进行操作

```shell
$ ./mongo
```
