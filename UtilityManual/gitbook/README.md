# Gitbook

gitbook 网站是一个简单的个人在线书籍网站，在这里可以把自己的文档整理成书籍发布出来，便于阅读。

查看 [Gitbook 官网](https://www.gitbook.com/)

## 安装 gitbook

使用 nodejs 包管理器 npm/cnpm 进行安装

```sh
npm install -g gitbook-cli
```

## 基本使用

1. 初始化一个 gitbook 项目

```sh
gitbook init
```

此时会生成两个文件

- SUMMARY.md 目录文件
- README.md

2. 安装插件

```sh
gitbook install
```

> 注意! 这种方法特别的慢,我们可以使用 cnpm 直接安装插件,然后在 book.json 里配置即可.
>
> ```sh
> cnpm install gitbook-plugin-pluginName
> ```
> 查看 [Gitbook 插件](./plugins.md)

查看项目，热编译

```sh
gitbook serve
chrome http://localhost:4000
```

编译项目

```sh
gitbook build
```

## 更多配置

查看 [book.json](./book.json.md)
