# ubuntu atom 安装包慢的问题

查看 [Atom 插件安装慢解决方案](https://blog.csdn.net/qq_33673284/article/details/80364799)

## apm 安装

apm (Atom Package Manager) 是 Atom 的包管理工具，可以方便的管理 Atom 的插件。
首先切换到 Atom 的插件目录。

> Atom 的插件目录为 C:\Users\zengqing\.atom\packages 注：此处 zengqing 更换为你的电脑用户名
> Ubuntu下为 /home/username/.atom/packages

执行命令：

```
$ apm install atom-package-name
```

然后静等片刻待出现 done 即表示安装成功,随后就可以打开 Atom 使用此插件了


## 切换到国内源

编辑 home 文件夹下的配置文件（若不存在，则创建）：

```
$ vim /home/username/.atom/.atomrc
```

修改内容：

```
registry = https://registry.npm.taobao.org
```

保存文件后可通过 apm install --check 命令测试是否可以正常安装，然后就可以去 Atom 里正常安装了
