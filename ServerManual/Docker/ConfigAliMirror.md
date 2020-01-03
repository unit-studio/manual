# Docker 配置阿里源

查看官网说明
[阿里云 镜像源](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors)

加速器地址:

```
https://fokh13t4.mirror.aliyuncs.com
```

## 步骤说明(主要针对Win10)

### 1. 安装／升级 Docker 客户端

对于 Windows 10 以下的用户，推荐使用 Docker Toolbox

Windows 安装文件：http://mirrors.aliyun.com/docker-toolbox/windows/docker-toolbox/

对于 Windows 10 以上的用户 推荐使用 Docker for Windows

Windows 安装文件：http://mirrors.aliyun.com/docker-toolbox/windows/docker-for-windows/

### 2. 配置镜像加速器

针对安装了 Docker Toolbox 的用户，您可以参考以下配置步骤：

创建一台安装有 Docker 环境的 Linux 虚拟机，指定机器名称为 unitstudio，同时配置 Docker 加速器地址。

```
docker-machine create --engine-registry-mirror=https://fokh13t4.mirror.aliyuncs.com -d virtualbox unitstudio
```

查看机器的环境配置，并配置到本地，并通过 Docker 客户端访问 Docker 服务。

```
docker-machine env unitstudio
eval "$(docker-machine env unitstudio)"
docker info
```

针对安装了 Docker for Windows 的用户，您可以参考以下配置步骤：
在系统右下角托盘图标内右键菜单选择 Settings，打开配置窗口后左侧导航菜单选择 Docker Daemon。编辑窗口内的 JSON 串，填写下方加速器地址：

```
{
  "registry-mirrors": ["https://fokh13t4.mirror.aliyuncs.com"]
}
```

编辑完成后点击 Apply 保存按钮，等待 Docker 重启并应用配置的镜像加速器。

注意
Docker for Windows 和 Docker Toolbox 互不兼容，如果同时安装两者的话，需要使用 hyperv 的参数启动。

```
docker-machine create --engine-registry-mirror=https://fokh13t4.mirror.aliyuncs.com -d hyperv unitstudio
```

Docker for Windows 有两种运行模式，一种运行 Windows 相关容器，一种运行传统的 Linux 容器。同一时间只能选择一种模式运行。

### 3. 相关文档

[Docker 命令参考文档](https://docs.docker.com/engine/reference/commandline/cli/?spm=5176.8351553.0.0.3ce91991ksmtAm)

[Dockerfile 镜像构建参考文档](https://docs.docker.com/engine/reference/builder/?spm=5176.8351553.0.0.3ce91991ksmtAm)


## 操作过程

创建一台安装有 Docker 环境的 Linux 虚拟机，指定机器名称为 unitstudio，同时配置 Docker 加速器地址。

```
李叶飞@DESKTOP-RS73EAQ MINGW64 /d/Program Files/Docker Toolbox
$ docker-machine create --engine-registry-mirror=https://fokh13t4.mirror.aliyuncs.com -d virtualbox unitsutdio
Running pre-create checks...
Creating machine...
(unitsutdio) Copying C:\Users\李叶飞\.docker\machine\cache\boot2docker.iso to C:\Users\李叶飞\.docker\machine\machines\unitsutdio\boot2docker.iso...
(unitsutdio) Creating VirtualBox VM...
(unitsutdio) Creating SSH key...
(unitsutdio) Starting the VM...
(unitsutdio) Check network to re-create if needed...
(unitsutdio) Windows might ask for the permission to configure a dhcp server. Sometimes, such confirmation window is minimized in the taskbar.
(unitsutdio) Waiting for an IP...
Waiting for machine to be running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH to be available...
Detecting the provisioner...
Provisioning with boot2docker...
Copying certs to the local machine directory...
Copying certs to the remote machine...
Setting Docker configuration on the remote daemon...
Checking connection to Docker...
Docker is up and running!
To see how to connect your Docker Client to the Docker Engine running on this virtual machine, run: D:\Program Files\Docker Toolbox\docker-machine.exe env unitsutdio
```

整体速度还行.

查看虚拟机状态:

```
李叶飞@DESKTOP-RS73EAQ MINGW64 /d/Program Files/Docker Toolbox
$ docker-machine env unitsutdio
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://192.168.99.101:2376"
export DOCKER_CERT_PATH="C:\Users\李叶飞\.docker\machine\machines\unitsutdio"
export DOCKER_MACHINE_NAME="unitsutdio"
export COMPOSE_CONVERT_WINDOWS_PATHS="true"
# Run this command to configure your shell:
# eval $("D:\Program Files\Docker Toolbox\docker-machine.exe" env unitsutdio)

李叶飞@DESKTOP-RS73EAQ MINGW64 /d/Program Files/Docker Toolbox
$ eval "$(docker-machine env default)"

李叶飞@DESKTOP-RS73EAQ MINGW64 /d/Program Files/Docker Toolbox
$ docker info
Containers: 0
 Running: 0
 Paused: 0
 Stopped: 0
Images: 0
Server Version: 19.03.5
Storage Driver: overlay2
 Backing Filesystem: extfs
 Supports d_type: true
 Native Overlay Diff: true
Logging Driver: json-file
Cgroup Driver: cgroupfs
Plugins:
 Volume: local
 Network: bridge host ipvlan macvlan null overlay
 Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
Swarm: inactive
Runtimes: runc
Default Runtime: runc
Init Binary: docker-init
containerd version: b34a5c8af56e510852c35414db4c1f4fa6172339
runc version: 3e425f80a8c931f88e6d94a8c831b9d5aa481657
init version: fec3683
Security Options:
 seccomp
  Profile: default
Kernel Version: 4.14.154-boot2docker
Operating System: Boot2Docker 19.03.5 (TCL 10.1)
OSType: linux
Architecture: x86_64
CPUs: 1
Total Memory: 989.5MiB
Name: default
ID: DOAT:4VEC:OMPZ:U27C:KOPT:ESQO:4OID:NNOZ:AW6A:ZDPD:BPWN:HTRZ
Docker Root Dir: /mnt/sda1/var/lib/docker
Debug Mode (client): false
Debug Mode (server): false
Registry: https://index.docker.io/v1/
Labels:
 provider=virtualbox
Experimental: false
Insecure Registries:
 127.0.0.0/8
Live Restore Enabled: false
```

设置配置文件:

```sh
##### 这个路径不对,别在这配置啊,老哥!!!!
# $HOME ==> /c/user/liyf 即 用户目录
# $ vim $HOME/.docker/daemon.json
##### 这个路径不对,别在这配置啊,老哥!!!!

# 添加配置
{
  "registry-mirrors": [
    "https://fokh13t4.mirror.aliyuncs.com",
    "http://hub-mirror.c.163.com/",
    "https://registry.docker-cn.com"
  ]
}
```

重启Docker.
