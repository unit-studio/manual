# Vue 使用vue-cli v2.x 进行项目构建(废弃)


![](assets/markdown-img-paste-20190527150942537.png)

安装 vue/cli-init

```shell
$ cnpm install -g @vue/cli
$ cnpm install -g @vue/cli-init
```

安装完成后,进行项目的创建

```shell
$ vue init webpack vue_workspace
```

在提示中选择要使用的功能,全选即可.

此时生成了一个简单的 vue 项目模板,执行以下命令进行启动项目

```shell
$ cd vue_workspace
$ npm start
```

可以看到执行结果

![](assets/markdown-img-paste-20190527152341961.png)

> 注意: 当在 main.js 中引入全局样式时,会报错
>
> ```
> This relative module was not found:
> * ~/css/style.scss in ./src/main.js
> ```
>
> 这是因为此模板不自带 `sass-loader`, 所以需要手动安装
> ![](assets/markdown-img-paste-20190527163256991.png)
