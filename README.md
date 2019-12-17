# unit-studio

Unit-studio's technical manual repo.

## Table of Contents

- [Background](#background)
- [Install](#install)
- [Usage](#usage)
- [Maintainers](#maintainers)
- [License](#license)

## Background

Transfer [previous repos](http://106.13.58.177:8081/) into GitHub.

## Install

此项目使用 [node](http://nodejs.org), [npm](https://npmjs.com) and [gitbook-cli](https://www.npmjs.com/package/gitbook-cli).
如果没有安装,请查看官网进行安装后再进行下面的步骤,其中建议使用 **cnpm** 替换掉 **npm**.

```sh
# 安装命令行工具 gitbook-cli
$ npm install gitbook-cli -g
```

## Usage

打开项目的过程(其中依赖包 node_modules 已经同时提交到了 repo 中,所以不必再次进行安装):

```sh
# 安装依赖,依赖包已传至repo,此步骤可省略
$ gitbook install

# 热启动服务
$ gitbook serve

# 编译项目
$ gitbook build
```

## Maintainers

[@unit-studio](https://github.com/unit-studio)

## License

[MIT](LICENSE) © unit-studio
