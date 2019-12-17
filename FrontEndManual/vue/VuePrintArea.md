# Vue 打印部分页面 vuePlugs_printjs 篇

查看 [vue 实现打印功能的两种方法](https://www.jb51.net/article/147040.htm)

这里简述已经测试过的用法,手动下载插件 [Github vuePlugs_printjs](https://github.com/xyl66/vuePlugs_printjs)

## vuePlugs_printjs (vue 打印插件)

**使用方法**

```js
import Print from '@/plugs/print'
Vue.use(Print) // 注册
<template>
<section ref="print">
	打印内容
	<div class="no-print">不要打印我</div>
</section>
</template>
this.$print(this.$refs.print) // 使用
```

<font color=#c00 >注意事项</font>

需使用 ref 获取 dom 节点，若直接通过 id 或 class 获取则 webpack 打包部署后打印内容为空

**指定不打印区域**

方法一. 添加 no-print 样式类

```HTML
<div class="no-print">不要打印我</div>
```

方法二. 自定义类名

```html
<div class="do-not-print-me-xxx">不要打印我</div>
```

```js
this.$print(this.$refs.print, { "no-print": ".do-not-print-me-xxx" }); // 使用
```

## 示例用法

首先,声明一个空白代码块,并赋予 **id** 和 **ref** 属性

```html
<template>
  ...
  <div v-show="false">
    <!-- 不要在要打印的元素上添加 v-if/v-show 等限制,否则在打印时元素显示不出来 -->
    <div id="preprint" ref="preprint"></div>
  </div>
  ...
</template>
```

在方法处,可以进行更多的设置

```js
// 在{}.methods中添加打印方法
printTable(tableId, tableName) {
	if (!tableId || !tableName) {
		this.errorMessage("打印: 引用错误!");
		return;
	}
	this.$confirm('若页面显示不全,请设置缩放', '提示', {
		type: "warning"
	})
	.then(mes => {
    // 找到空元素,这里使用 getElementById 来找元素,不使用 ref 了
		let preprintElement = document.getElementById('preprint');
    // 将元素内容清空,否则在上次打印后,会有残余
		preprintElement.innerHTML = '';

    // 这这里添加需要打印的元素,注意,都需要使用 element,不要用字符串
		let tableElementTitle = document.createElement('h1');
		tableElementTitle.innerText = `${tableName}`;
    // 找到要打印的元素,不能直接取他的值,必须使用 cloneNode(true) 来复制一个,否则在下边 append 后,会移除掉之前的元素
    let tableElement = document.getElementById(tableId).cloneNode(true);

    // 将创建和找到的元素添加到打印元素里边
		preprintElement.appendChild(tableElementTitle);
    preprintElement.appendChild(tableElement)

    // 已经将要打印的部分页面放到打印元素中了,使用插件打印.
		this.$print(preprintElement)
	})
	.catch(error => {
		this.errorMessage("打印: 取消")
	});
},
```
