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

[@unit-studio](https://github.com/unit-studio)

## License

[MIT](LICENSE) © unit-studio
