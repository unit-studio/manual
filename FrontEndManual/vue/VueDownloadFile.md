# Vue 下载文件

### 调用 window.open

先写个触发按钮:

```
<el-button @click="download" >导出</el-button>
```

然后引用必要的 npm 包, 查看 [qs](https://www.npmjs.com/package/qs), 设置一下链接地址以及参数信息

```
import qs from 'qs'
import { setBaseUrl } from '@/config.js'
.....
getExportLink (params = {}){
    let link = setBaseUrl() +'/api/export';
    // 设置全局参数
    params.appId=process.env.appId;
    let url=link+'?'+qs.stringify(params);
    return url;
}
```

导出函数如下

```
download(){
    let _exportLink = getExportLink ({
        // 设置独有参数
        self_defined_params: xxx
    })
    // 在新的网页打开导出链接即可实现下载
    window.open( _exportLink, "_blank" );
}
```

### 使用 \<a\> 标签

获取下载链接,同上

```
import qs from 'qs'
import { setBaseUrl } from '@/config.js'
.....
getExportLink (params = {}){
    let link = setBaseUrl() +'/api/export';
    // 设置全局参数
    params.appId=process.env.appId;
    let url=link+'?'+qs.stringify(params);
    return url;
}
```

直接在 href 属性中设置下载链接

```
<a :href="exportLink()" >导出</a>
```

即可.
