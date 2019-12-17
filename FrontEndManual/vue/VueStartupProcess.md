# Vue 项目启动过程分析

将项目从开始启动,到生成可运行代码的过程记录在此.

## npm start

首先,需要了解一下 **npm** 命令,请查看 [NPM 官网](https://www.npmjs.cn/)

在开发版本中,使用 `npm start` 命令运行此项目.
在 package.json 文件中定义的 "scripts" 对象中查找 "start" 属性， 如果此属性定义了任何命令则执行之。 如果 "scripts" 对象中没有定义 "start" 属性， 默认执行 node server.js 命令。
找到对应的命令:

```
  "scripts": {
    "dev": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js",
    "start": "npm run dev",
    "unit": "jest --config test/unit/jest.conf.js --coverage",
    "e2e": "node test/e2e/runner.js",
    "test": "npm run unit && npm run e2e",
    "build": "node build/build.js"
  },
```

即执行了 `npm run dev` 命令,其中 `npm run` 是 `npm run-script` 的别名,故实际执行了 `npm run-script dev`. 这会执行 package.json 中定义的 scripts.dev 指定的命令,故最终执行的命令为

```
$ webpack-dev-server --inline --progress --config build/webpack.dev.conf.js
```

接下来就转到了 webpack 的配置上.

## webpack

首先,需要了解一下 **webpack**,这是一个现在最流行的代码打包工具,可进入 [webpack 中文网](https://www.webpackjs.com/) 学习使用.
然后,仔细阅读 [webpack-dev-server 的使用](https://www.webpackjs.com/guides/development/#%E4%BD%BF%E7%94%A8-webpack-dev-server)
简而言之, webpack-dev-server 提供了一个 基于 webpack 的可以热加载的 WEB 服务器.

### 配置文件

找到配置文件 build/webpack.dev.conf.js, 可以逐行阅读,这个文件一共也不到 100 行.
先看导出:

```
module.exports = new Promise((resolve, reject) => {
  portfinder.basePort = process.env.PORT || config.dev.port
  portfinder.getPort((err, port) => {
      ....
      resolve(devWebpackConfig)
    }
  })
})
```

发现返回了一个变量 devWebpackConfig, 找到定义:

```
const config = require('../config')
const merge = require('webpack-merge')
const baseWebpackConfig = require('./webpack.base.conf')
const HtmlWebpackPlugin = require('html-webpack-plugin')
....
const devWebpackConfig = merge(baseWebpackConfig, {
  ....
  // these devServer options should be customized in /config/index.js
  devServer: {
    ....
    host: HOST || config.dev.host,
    port: PORT || config.dev.port,
    ....
  },
  plugins: [
    ....
    // https://github.com/ampedandwired/html-webpack-plugin
    new HtmlWebpackPlugin({
      filename: 'index.html',
      template: 'index.html',
      inject: true
    }),
    ....
  ]
})
```

由此可见 devWebpackConfig 是在 ./webpack.base.conf 的基础上,通过 webpack-merge 工具进行进一步合并的.

根据 devServer.host 和 devServer.port 可以找到使用 webpack-dev-server 启动的服务器或在哪里启动.
查看 root/config/index.js ,找到配置

```
module.exports = {
  dev: {
    ....
    host: 'localhost', // can be overwritten by process.env.HOST
    port: 8080, // can be overwritten by process.env.PORT, if port is in use, a free one will be determined
    ....
  },
  ....
}
```

> 这样我们可以得出启动的 WEB 服务会在 `localhost:8080` 启动,这也是之后使用浏览器访问的地址.
> 同时我们发现使用了插件 [HtmlWebpackPlugin](https://github.com/ampedandwired/html-webpack-plugin)
> 阅读对应文档可知,这个插件规定了这个项目要使用的 html 模板: `root/index.html` ,当 webpack 将项目文件打包完以后,会以 `<script>标签` 的形式插入到 html 文件中

查看 webpack.base.conf, 可以看到

```
const config = require('../config')
....
module.exports = {
  context: path.resolve(__dirname, '../'),
  entry: {
    app: './src/main.js'
  },
  output: {
    path: config.build.assetsRoot,
    filename: '[name].js',
    publicPath: process.env.NODE_ENV === 'production'
      ? config.build.assetsPublicPath
      : config.dev.assetsPublicPath
  },
  ....
}
```

项目入口为 `root/src/main.js`, 出口为 `require('../config').build.assetsRoot`, 可以浏览此文件得出,项目出口为 `root/dist`.

### webpack 配置总结

由上述配置可见,此项目使用 webapck 进行项目打包和构建.
以 `root/index.html` 为模板, 以 `root/src/main.js` 为打包入口, 以 `root/dist/` 为打包出口.
WEB 服务启动位置为 `localhost:8080` .
但是在使用 webpack-dev-server 进行本地项目启动时,所有的打包好的文件均保存在内存中,没有生成实际的磁盘文件,故打包结果以 **浏览器可访问** 为准.
