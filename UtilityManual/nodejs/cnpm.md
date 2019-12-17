# cnpm #

## cnpm简介 ##

cnpm是npm的一个国内镜像,在中国境内进行开发时,使用cnpm来代替npm,可以大大提高包管理速度.

官方网站:
+ [cnpm 官网](https://npm.taobao.org/)

## cnpm使用说明 ##

1. 使用 cnpm (gzip 压缩支持) 命令行工具代替默认的 npm:

```
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```

2. 直接通过添加 npm 参数 alias 一个新命令:

```
$ alias cnpm="npm --registry=https://registry.npm.taobao.org --cache=$HOME/.npm/.cache/cnpm --disturl=https://npm.taobao.org/dist --userconfig=$HOME/.cnpmrc"

# Or alias it in .bashrc or .zshrc

$ echo '
#alias for cnpm
alias cnpm=\"npm --registry=https://registry.npm.taobao.org \
  --cache=$HOME/.npm/.cache/cnpm \
  --disturl=https://npm.taobao.org/dist \
  --userconfig=$HOME/.cnpmrc"' >> ~/.zshrc && source ~/.zshrc
```

建议使用第一种,简单,不容易出错.
