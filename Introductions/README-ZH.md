# unit-studio

此文档提供技术手册与故事记录.

查看 [English Version](/README.md)

## 目录

- [背景](#背景)
- [安装与初始化](#安装与初始化)
- [使用方法](#使用方法)
- [维护人员](#维护人员)
- [许可证](#许可证)

## 背景

将 [原有的项目](http://106.13.58.177:8081/) 转存到 Github.

## 安装与初始化

此项目使用 [node](http://nodejs.org), [npm](https://npmjs.com) and [gitbook-cli](https://www.npmjs.com/package/gitbook-cli).

如果没有安装,请查看官网进行安装后再进行下面的步骤,其中建议使用 **cnpm** 替换掉 **npm**.

```sh
# 安装命令行工具 gitbook-cli
$ npm install gitbook-cli -g
```

## 使用方法

打开项目的过程:

```sh
# 安装依赖,依赖包已传至repo,此步骤可省略
$ cnpm install
```
> **注意:**
> 不要执行 `gitbook install` 去安装依赖,这个太慢了
> 我们已经将所需的依赖提取出来,放到了 package.json
> 你通过 `cnpm install` 安装就好了

```sh
# 热启动服务
$ gitbook serve

# 编译项目
$ gitbook build
```

## 维护人员

[@unit-studio](https://github.com/unit-studio)

## 许可证

[MIT](LICENSE) © [unit-studio](https://github.com/unit-studio)
