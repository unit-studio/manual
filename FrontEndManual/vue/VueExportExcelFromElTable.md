# Vue 从 el-table 导出 excel

分为三步:

1. 导入必要的 npm 包

- [file-saver](https://www.npmjs.com/package/file-saver)
- [xlsx](https://www.npmjs.com/package/xlsx)

2. 在表格标签中设置 id
3. 按照以下方法导出

```
<template>
<section>
  <!-- 表格,设置id字段 -->
  <el-table :data="tableData" stripe style="width: 100%" @selection-change="checkIds" id="logTable">
    <el-table-column type="selection" width="65" align="center" :selectable="row => (row.state == '0')"></el-table-column>
    <el-table-column type="index" width="65" align="center"></el-table-column>
    <el-table-column prop="month" label="月份" align="center"></el-table-column>
    <el-table-column prop="amount" label="金额(元)" align="center"></el-table-column>
    <el-table-column prop="state" label="状态" align="center">
      <div slot-scope="scope">
        <span v-if="scope.row.state && scope.row.state == '0'">初始</span>
        <span v-if="scope.row.state && scope.row.state == '1'">已提交</span>
        <span v-if="scope.row.state && scope.row.state == '2'">初审通过</span>
        <span v-if="scope.row.state && scope.row.state == '3'">复审通过</span>
      </div>
    </el-table-column>
  </el-table>
</section>
</template>
<script>
// 引入需要的npm包
import FileSaver from 'file-saver';
import XLSX from 'xlsx';
export default {
  methods: {
    // 导出数据
    exportExcel() {
      /* generate workbook object from table */
      let wb = XLSX.utils.table_to_book(document.querySelector('#logTable'))
      /* get binary string as output */
      let wbout = XLSX.write(wb, {
        bookType: 'xlsx',
        bookSST: true,
        type: 'array'
      })
      try {
        let newBlob = new Blob([wbout], {
          type: 'application/octet-stream'
        })
        FileSaver.saveAs(newBlob, '导出名称.xlsx')
      } catch (e) {
        if (typeof console !== 'undefined') console.log(e, wbout)
      }
      return wbout
    },
  },
  created() {
    this.tableData = [{
      ...
    }]
  }
};
</script>
<style>
</style>
```

> 注意,不要在要导出的表格中使用 fixed 属性,这样会导致导出的数据重复
