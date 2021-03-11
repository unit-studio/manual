# unit-studio

My technical manual repo.

Checkout [中文版本](Introductions/README-ZH.md)

## Table of Contents

- [Background](#background)
- [Install](#install)
- [Usage](#usage)
- [Maintainers](#maintainers)
- [License](#license)

## Background

Transfer [previous repos](http://106.13.58.177:8081/) into GitHub.

## Install

This project uses [node](http://nodejs.org), [npm](https://npmjs.com) and [gitbook-cli](https://www.npmjs.com/package/gitbook-cli).

If these packages aren't installed locally,please install them by their website.

we recommand you to replace **npm** with **cnpm**.

```sh
# 安装命令行工具 gitbook-cli
$ npm install gitbook-cli -g
```

## Usage

Follow the steps:

```sh
# intall dependencies
$ cnpm install
```
> **Attention**:
> Do not run `gitbook install`, it takes too much time.
> And we've already reorganized the dependencies into package.json
> S.t. you shall install them with `cnpm install`

```sh
# start sceive
$ gitbook serve

# build project
$ gitbook build
```

## Maintainers

[@liyf7218](https://github.com/liyf7218)

## License

[MIT](LICENSE) © liyf7218
