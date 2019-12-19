# JS 对象数组去重

## 用 Array.prototype.filter

```js
function objectArrayDeduplication(arr) {
    // 需要一个字典，可以用 Set/WeakSet 或者就简单的 JS 对象
    const dict = {};

    // 过滤的过程中完善 dict
    return arr.filter(ele => {
        // 找到用来标识的字段
        let { key } = ele;

        // 检查如果字典中已经存在，那这个数据就过滤掉，不需要了
        if (dict[key]) {
            return false;
        }

        // 如果字典不不存在，加入字典，同时把数据保留下来（返回 true）
        dict[key] = true;
        return true;
    });
}
```
