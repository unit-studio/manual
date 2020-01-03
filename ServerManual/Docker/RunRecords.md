# Docker 运行记录 Win10 家庭版

## 初次运行记录

双击快捷方式 `Docker Quickstart Terminal`,初次启动 Docker.

```
Creating CA: C:\Users\李叶飞\.docker\machine\certs\ca.pem
Creating client certificate: C:\Users\李叶飞\.docker\machine\certs\cert.pem
Running pre-create checks...
(default) Image cache directory does not exist, creating it at C:\Users\李叶飞\.docker\machine\cache...
(default) No default Boot2Docker ISO found locally, downloading the latest release...
(default) Latest release for github.com/boot2docker/boot2docker is v19.03.5
(default) Downloading C:\Users\李叶飞\.docker\machine\cache\boot2docker.iso from https://github.com/boot2docker/boot2docker/releases/download/v19.03.5/boot2docker.iso...

===> Wait for a long time.....
```

这个太慢啦,有事限制访问的问题,需要翻翻墙.

> 如果不想翻墙,需要手动下载提示里边的版本,这里是 `https://github.com/boot2docker/boot2docker/releases/download/v19.03.5/boot2docker.iso` ,然后将其放到指定路径下 `C:\Users\李叶飞\.docker\machine\cache\boot2docker.iso`.

重新打开 `Docker Quickstart Terminal`,再次启动 Docker.

```
...
Starting "default"...
(default) Check network to re-create if needed...
(default) Windows might ask for the permission to configure a dhcp server. Sometimes, such confirmation window is minimized in the taskbar.
(default) Waiting for an IP...

===> Wait for another long time.....
```

这里就更难受了,半天也没动静.

> 查看 [stackoverflow docker-terminal-waiting-for-an-ip](https://stackoverflow.com/questions/35958619/docker-terminal-waiting-for-an-ip)

> [naitsirhc](https://stackoverflow.com/users/345236/naitsirhc): I had the same issue. I managed to get past the problem through the following steps:
>
> 1. Start the Oracle VM VirtualBox desktop application.
> 2. Select and manually start default virtual machine.
> 3. Close virtual machine window and choose to Send shutdown signal.
> 4. Run Docker Quickstart Terminal.
> 5. (optional) Right-click on default virtual machine and select Showin the Oracle VM VirtualBox desktop application to monitor virtual machine boot process.
>
> After performing the steps above, I the Docker Quickstart Terminal window displayed:
>
> ```
>                     ##         .
>                   ## ## ##        ==
>                ## ## ## ## ##    ===
>            /"""""""""""""""""\___/ ===
>       ~~~ {~~ ~~~~ ~~~ ~~~~ ~~~ ~ /  ===- ~~~
>            \______ o           __/
>              \    \         __/
>               \____\_______/
>
> docker is configured to use the default machine with IP 192.168.99.100
> For help getting started, check out the docs at https://docs.docker.com
>
> Start interactive shell
> ...
> ```

```
Machine "default" was started.
Waiting for SSH to be available...
Detecting the provisioner...
Started machines may have new IP addresses. You may need to re-run the `docker-machine env` command.
Regenerate TLS machine certs?  Warning: this is irreversible. (y/n): Regenerating TLS certificates
Waiting for SSH to be available...
Detecting the provisioner...
Copying certs to the local machine directory...
Copying certs to the remote machine...
Setting Docker configuration on the remote daemon...

This machine has been allocated an IP address, but Docker Machine could not
reach it successfully.

SSH for the machine should still work, but connecting to exposed ports, such as
the Docker daemon port (usually <ip>:2376), may not work properly.

You may need to add the route manually, or use another related workaround.

This could be due to a VPN, proxy, or host file configuration issue.

You also might want to clear any VirtualBox host only interfaces you are not using.
Error checking TLS connection: Error checking and/or regenerating the certs: There was an error validating certificates for host "192.168.99.100:2376": dial tcp 192.168.99.100:2376: i/o timeout
You can attempt to regenerate them using 'docker-machine regenerate-certs [name]'.
Be advised that this will trigger a Docker daemon restart which might stop running containers.

Error checking TLS connection: Error checking and/or regenerating the certs: There was an error validating certificates for host "192.168.99.100:2376": dial tcp 192.168.99.100:2376: i/o timeout
You can attempt to regenerate them using 'docker-machine regenerate-certs [name]'.
Be advised that this will trigger a Docker daemon restart which might stop running containers.

                        ##         .
                  ## ## ##        ==
               ## ## ## ## ##    ===
           /"""""""""""""""""\___/ ===
      ~~~ {~~ ~~~~ ~~~ ~~~~ ~~~ ~ /  ===- ~~~
           \______ o           __/
             \    \         __/
              \____\_______/

docker is configured to use the default machine with IP 192.168.99.100
For help getting started, check out the docs at https://docs.docker.com

Start interactive shell

李叶飞@DESKTOP-RS73EAQ MINGW64 /d/Program Files/Docker Toolbox
$
```

至此,Docker 启动成功.

## 再次运行记录

```
Error checking TLS connection: Error checking and/or regenerating the certs: There was an error validating certificates for host "192.168.99.100:2376": dial tcp 192.168.99.100:2376: i/o timeout
You can attempt to regenerate them using 'docker-machine regenerate-certs [name]'.
Be advised that this will trigger a Docker daemon restart which might stop running containers.

Error checking TLS connection: Error checking and/or regenerating the certs: There was an error validating certificates for host "192.168.99.100:2376": dial tcp 192.168.99.100:2376: i/o timeout
You can attempt to regenerate them using 'docker-machine regenerate-certs [name]'.
Be advised that this will trigger a Docker daemon restart which might stop running containers.

===> Wait a moment...
```

这里需要等一哈,他自己个会各种操作的,这个挺好~~~

```
===> Then it turns up...

                        ##         .
                  ## ## ##        ==
               ## ## ## ## ##    ===
           /"""""""""""""""""\___/ ===
      ~~~ {~~ ~~~~ ~~~ ~~~~ ~~~ ~ /  ===- ~~~
           \______ o           __/
             \    \         __/
              \____\_______/

docker is configured to use the default machine with IP 192.168.99.100
For help getting started, check out the docs at https://docs.docker.com

Start interactive shell

李叶飞@DESKTOP-RS73EAQ MINGW64 /d/Program Files/Docker Toolbox
$
```

至此,Docker 启动成功,不需要任何的操作~~~
