# Ubuntu 安装MongoDB 管理工具 Robo3T

## 下载安装包

下载地址： [https://download-test.robomongo.org/linux/robo3t-1.3.1-linux-x86_64-7419c406.tar.gz](https://download-test.robomongo.org/linux/robo3t-1.3.1-linux-x86_64-7419c406.tar.gz)

运行文件： 解压到当前目录，执行 ./bin/robo3t 即可。

```shell
$ wget https://download-test.robomongo.org/linux/robo3t-1.3.1-linux-x86_64-7419c406.tar.gz
$ tar -zxvf robo3t-1.3.1-linux-x86_64-7419c406.tar.gz

# 运行
$ ./robo3t-1.3.1-linux-x86_64-7419c406.tar.gz/.bin/robo3t

# 或者将其倒入配置文件
$ vim /etc/profile # 添加一行， PATH=$PATH:/usr/local/packages/robo3t-1.3.1-linux-x86_64-7419c406/bin

```

运行时可能会报错：

> 
