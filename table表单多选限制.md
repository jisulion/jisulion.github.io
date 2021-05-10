#### 内容限制

```js
<el-table
        ref="multipleTable"
        :data="tableData"
        class="base-data-table"
        style="width:100%"
        :row-style="{background:'#0c0f38',color:'#999'}"
        :header-cell-style="{background:'#12164f',color:'#fff'}"
        @selection-change="handleSelectionChange"
      >
 //需要隐藏掉多选
```



```js
   handleSelectionChange(val) {
      if (val.length > 4) {
        this.$message.error("最只能多选四项");
        // return;
        this.effectArray = val.slice(0, 4);
        let tempArr = val.slice(4);
        if (tempArr.length !== 0) {
          tempArr.forEach((ele) => {
            this.$refs.multipleTable.toggleRowSelection(ele, false);
          });
        }
      } else {
        this.effectArray = val;
      }
    },
```

