# 关闭后台运行的程序

## 查找运行的程序

有两个命令可以用，jobs和ps,区别是jobs用于查看当前终端后台运行的任务，换了终端就看不到了。而ps命令用于查看瞬间进程的动态，可以看到别的终端运行的后台进程

```shell
$ jobs
  # 由于之前已经通过exit退出了终端,所以没东西
$ ps -aux | grep "http-server"
qx        3266  0.0  0.0 112708   988 pts/0    R+   10:47   0:00 grep --color=auto http-server
root     12065  0.0  3.6 612600 36572 ?        Sl   Aug28   0:06 node ../append_packages/node-v10.16.3-linux-x64/bin/http-server . -p 8080
qx       32635  0.0  3.2 679824 33460 ?        Sl   Sep01   0:03 node /usr/local/bin/http-server . -p 8090
```

> ps: 查看当前的所有进程
> 参数: a:显示所有程序  u:以用户为主的格式来显示   x:显示所有程序，不以终端机来区分

## 执行终止命令

kill命令：结束进程

-   通过jobs命令查看jobnum，然后执行   kill %jobnum
-   通过ps命令查看进程号PID，然后执行  kill %PID
-   如果是前台进程的话，直接执行 Ctrl+c 就可以终止了

```shell
kill 32635
```

## 前后台进程的切换与控制

-   **fg命令**
    功能：将后台中的命令调至前台继续运行
    如果后台中有多个命令，可以先用jobs查看jobnun，然后用 fg %jobnum 将选中的命令调出。

-   **Ctrl + z 命令**
    功能：将一个正在前台执行的命令放到后台，并且处于暂停状态

-   **bg命令**
    功能：将一个在后台暂停的命令，变成在后台继续执行
    如果后台中有多个命令，可以先用jobs查看jobnum，然后用 bg %jobnum 将选中的命令调出继续执行。
