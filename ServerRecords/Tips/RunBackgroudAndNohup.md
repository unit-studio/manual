# 程序放后台运行

## Linux系统把程序放后台运行，后台执行不退出，退出终端仍运行进程，继续运行

Linux下把程序放到后台运行，相关的命令，如下：

 

1. 把程序放后台运行，简单的话，只要在命令后面加一个“&”， 如：
    ```shell
    http-server . -p 8080 &
    ```

2. 或者在运行命令后，按一下 Ctrl+Z，如运行 `http-server . -p 8080` 后，按一下 Ctrl+Z

3. 程序在后台运行了，但还是看到输出信息，可以用管道命令把输出定向到 /dev/null，如：
    ```shell
    http-server . -p 8080 >/dev/null
    ```

4. 普通的输出信息看不到了，但还是看到一些信息，如错误信息等，需要再添加 2>&1 命令，如：
    ```shell
    http-server . -p 8080 >/dev/null 2>&1
    ```

5. 程序在后台运行了，但退出当前会话，发现程序还是停止了，此时要用nohup命令，如：
    ```shell
    nohup http-server . -p 8080 >/dev/null 2>&1 
    ```

6. 使用nohup后，应确保用exit命令退出当前账户，非常正常退出或结束当前会话，在后台运行的作业也会终止

7. 命令在后台运行了，怎么查看？使用jobs命令可列出当前会话的后台任务，jobs -l 能查看到 PID，进而可以用kill终止某个任务

8. 是终命令可能是：
    ```shell
    nohup http-server . -p 8080 >/dev/null 2>&1 &
    ```
 

### 注: 上面命令中“2>&1”，这里的2和1是啥？参考如下：

其中 0、1、2分别代表如下含义：

0 – stdin (standard input)

1 – stdout (standard output)

2 – stderr (standard error)
