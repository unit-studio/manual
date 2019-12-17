# Vue 项目执行流程分析

此处记录 vue 文件从最顶端开始的组建调用过程.

## 入口文件

由 [项目执行流程分析(启动过程)](#31) 得知,入口文件为 `root/src/main.js`
查看此文件,分析其实现了哪些功能.

```
import Vue from 'vue'
import App from './App'
import router from './router'

Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  render: h => h(App)
})
```

### 挂载

首先,也是最重要的,就是挂载.
查看 [Vue 选项/DOM el](https://cn.vuejs.org/v2/api/#el)
创建了一个新的 Vue 实例,将其挂载到了 id 为 app 的节点上,考虑到 webpack 打包完成后会将 vue 项目以 `<script> 标签` 的形式插入到指定的 html 中,此挂载功能是最为紧要的,由此建立起了整个 vue 项目与实际 html 文件的连接.

> 提供一个在页面上已存在的 DOM 元素作为 Vue 实例的挂载目标。可以是 CSS 选择器，也可以是一个 HTMLElement 实例。
> 在实例挂载之后，元素可以用 vm.$el 访问。
> 如果在实例化时存在这个选项，实例将立即进入编译过程，否则，需要显式调用 vm.$mount() 手动开启编译。
> 如果在 html 模板文件中没有声明 id 为 app 的节点,那么整个项目也并不会有任何的报错,但是页面会是 html 模板原有的模样,即一片空白

注意!

> 提供的元素只能作为挂载点。不同于 Vue 1.x，所有的挂载元素会被 Vue 生成的 DOM 替换。因此不推荐挂载 root 实例到 html 或者 body 上。

### 渲染

查看 [Vue 选项/DOM render](https://cn.vuejs.org/v2/api/#render)
字符串模板的代替方案，允许你发挥 JavaScript 最大的编程能力。该渲染函数接收一个 createElement 方法作为第一个参数用来创建 VNode

> render 的类型为 (createElement: () => VNode) => VNode,在应用时可用匿名函数展示 render: createElement => createElement(<vue-component />)
> Vue 选项中的 render 函数若存在，则 Vue 构造函数不会从 template 选项或通过 el 选项指定的挂载元素中提取出的 HTML 模板编译渲染函数

### 绑定路由

查看 [Vue-Router Getting Started](https://router.vuejs.org/guide/#html)
路由会作为插件引入到 Vue 项目中,引入插件需要以下几步:

```
// 0. If using a module system (e.g. via vue-cli), import Vue and VueRouter
// and then call `Vue.use(VueRouter)`.

// 1. Define route components.
// These can be imported from other files
const Foo = { template: '<div>foo</div>' }
const Bar = { template: '<div>bar</div>' }

// 2. Define some routes
// Each route should map to a component. The "component" can
// either be an actual component constructor created via
// `Vue.extend()`, or just a component options object.
// We'll talk about nested routes later.
const routes = [
  { path: '/foo', component: Foo },
  { path: '/bar', component: Bar }
]

// 3. Create the router instance and pass the `routes` option
// You can pass in additional options here, but let's
// keep it simple for now.
const router = new VueRouter({
  routes // short for `routes: routes`
})

// 4. Create and mount the root instance.
// Make sure to inject the router with the router option to make the
// whole app router-aware.
const app = new Vue({
  router
}).$mount('#app')

// Now the app has started!
```

绑定插件时,使用了 Vue.use(Plugin) 方法,来声明要使用此插件,但是有一个疑惑:
在 router/index.js 中使用了 Vue.use(vue-router) , 这个 Vue 是此文件使用 import('vue')来引入的,是一次独立的引用,然后抛出了一个新的 Router 实例.
main.js 引入此实例后可以直接使用
直观的看来,这两个文件分别引入了 Vue 包,但是功能可以连贯的实现,百思不得其解,有必要查看一下源码.
在 vue 源码文件夹中查找 [ 'vue.use:' , 'vue.use=' , 'vue.use =' ,...]可以找到源码文件( node_modules\vue\src\core\global-api\use.js )

```
/* @flow */

import { toArray } from '../util/index'

export function initUse (Vue: GlobalAPI) {
  Vue.use = function (plugin: Function | Object) {
    const installedPlugins = (this._installedPlugins || (this._installedPlugins = []))
    if (installedPlugins.indexOf(plugin) > -1) {
      return this
    }

    // additional parameters
    const args = toArray(arguments, 1)
    args.unshift(this)
    if (typeof plugin.install === 'function') {
      plugin.install.apply(plugin, args)
    } else if (typeof plugin === 'function') {
      plugin.apply(null, args)
    }
    installedPlugins.push(plugin)
    return this
  }
}

```

可以看到这个函数的功能是 `touch` 一下传入的插件,有就返回,没有就标识一下,没有其他多余的功能.
所以 Vue.use(Plugin)只是单纯的判断要插入的插件是否已经存在了,避免重复插入.
