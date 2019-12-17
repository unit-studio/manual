# 搭建 Git 仓库

## 安装Git

在服务器和客户端都要安装 Git

查看: [安装 Git](/Server/LinuxPackages/GitInstall.md)

## 服务器端

### 1. 创建用户

```shell
$ useradd git #新建用户
$ passwd git  #修改用户密码
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
```

### 2. 新建git仓库

```shell
$ cd /usr/local/git_repos
$ git init --bare qx_documents.git #使用 --bare 创建裸仓库,一般裸仓库以 .git 为后缀
$ ls
qx_documents.git
```

### 3. 将git仓库的owner改为前面创建的git账户

```shell
$ chown -R git:git qx_documents.git/
```

这样就可以使用远程克隆此git仓库了.

## 客户端

-  调出 bash/gitBash,使用命令克隆

    ```shell
    $ git clone git@106.13.58.177:/usr/local/git_repos/qx_documents.git qx_documents
    Cloning into 'qx_documents'...
    The authenticity of host '106.13.58.177 (106.13.58.177)' can't be established.
    ECDSA key fingerprint is SHA256:VaIbnZhPZy7k1iJrAPKlwHFOswDfadk3hzIDfam4Oxs.
    Are you sure you want to continue connecting (yes/no)? y
    Please type 'yes' or 'no': yes
    Warning: Permanently added '106.13.58.177' (ECDSA) to the list of known hosts.
    git@106.13.58.177's password:
    warning: You appear to have cloned an empty repository.

    $ ls qx_documents #查看仓库内部文件
    #(寐有东西)
    ```

- 第一次链接服务器上时会提示保存身份信息,输入 `yes` ,回车即可.此时会在 C:\\Users\\UserName.ssh\\ 下发现多出来一个文件 known_hosts,以后在这台电脑上再次连接目标 Git 服务器时不会再提示上面的语句。

- clone项目时会提示输入密码，直接输入在服务端创建git账号时填写的密码即可。

**这样的设置有一个弊端,在每次需要进行远程操作的的时候,都需要输入密码.**
