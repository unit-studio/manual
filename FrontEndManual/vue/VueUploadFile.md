# Vue 上传文件

### 使用 Element 组件库

使用 [element-ui upload 组件](http://element-cn.eleme.io/2.0/#/zh-CN/component/upload),一行代码如下

```
<el-upload action="https://jsonplaceholder.typicode.com/posts/" :on-change="handleChange" :file-list="fileList" ></el-upload>
```
