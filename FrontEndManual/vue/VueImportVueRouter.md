# Vue 使用 vue-router

## 引用路由

详细理解路由的过程,可以先查看 [vue-router 中文官网](https://router.vuejs.org/zh/)
一般来说,引入路由一般需要四步:

1. 引入 vue 和 vue-router
2. 声明我们这个项目这就要使用路由,使用 `Vue.use(Router)`
3. 创建独立的路由实例,进行适当的配置,使用 `new Router(config)`, 查看 /src/router/index.js:

   ```
   import Vue from 'vue'
   import Router from 'vue-router'
   import { routes } from './routes'

   Vue.use(Router)

   export default new Router({
     routes
   })
   ```

4. 至此,路由仍没有绑定到任何的 Vue 实例中,所以需要引入创建好的路由然后绑定一下,使用 `new Vue({router, ....})`, 查看 /src/main.js:

   ```
   import Vue from 'vue'
   import router from './router'
   ....
   new Vue({
     router, ....
   })
   ```

## 路由的配置

路由的配置相当于组织整体项目和页面的总规划,不可避免的要使用到以下功能:

- 路径导航
- 嵌套路由
- 路由懒加载
- ...

从最基本的路由配置入手,先定义一个最简单的路由,当页面只想 /demo 时,在 main-body 处显示组件 /src/views/demo/index.vue
编辑 vue-router 的配置文件 /src/router/routes.js :

```
import IContainer from '@/containers'
// 导出路由
export const routes = [
  {
    path: '/',
    name: 'IContainer',
    component: IContainer,
    redirect: '/demo',
    children: [
      {
        path: '/demo',
        name: 'Demo',
        component: resolve => require(['@/views/demo'], resolve)
      }
    ]
  }
]
```

vue-router 最基本的路由配置为:

```
{
    path: '/xxx',
    name: 'xxx',
    component: VueComponent
}
```

这样就能简单的使用路由了.
进一步使用 [嵌套路由](https://router.vuejs.org/zh/guide/essentials/nested-routes.html) 的话,需要配置 children 属性,当启用此属性时,还需要在父组件内部配合添加路由组件,查看 src/containers/index.vue:

```
<template>
    <parent-components>
        ....
        <router-view />
    </parent-components>
</template>
```

当路由导航到指定的子组件时,会先渲染父组件,然后将子组件添加到 `<router-view />` 所处的位置,即 进行替换.

当有了嵌套路由 时,必然也要有导向内部组件的 [重定向功能](https://router.vuejs.org/zh/guide/essentials/redirect-and-alias.html),那么就需要使用 redirect 属性, 于是可以得到 routes.js 文件中的大部分配置.

然后是懒加载,可以查看 [vue-router 懒加载功能](https://router.vuejs.org/zh/guide/advanced/lazy-loading.html)

> 为什么需要懒加载？
> 像 vue 这种单页面应用，如果没有应用懒加载，运用 webpack 打包后的文件将会异常的大，造成进入首页时，需要加载的内容过多，时间过长，会出啊先长时间的白屏，即使做了 loading 也是不利于用户体验，而运用懒加载则可以将页面进行划分，需要的时候加载页面，可以有效的分担首页所承担的加载压力，减少首页加载用时
> 简单的说就是：进入首页不用一次加载过多资源造成用时过长！！！

先看一下 [CSDN 博客 vue 路由懒加载](https://blog.csdn.net/weixin_38704338/article/details/79103230), 这里有讲 vue 路由懒加载的原理和过程.
**在这里也要抛出一个疑问** ,为什么会是如下的写法:

```
    component: resolve => require(['@/views/demo'], resolve)
```

反正是能用,很难受,抽时间读一读源码.

## 独立页面的配置

### ErrorPage

路由的配置是从上到下依次检测的,所以可以将 ErrorPage 页面放到路由最底部. 打开 /src/router/routes.js

```
import ErrorPage from '@/components/404'
....
export const routes = {
    ....
    ,{
        path: '*',
        name: 'ErrorPage',
        component: ErrorPage
    }
}
```

使用通配符,当前面的路由都不匹配时,会调整到 ErrorPage.
