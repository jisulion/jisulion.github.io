```html
 <el-table :key="'collapseTable-' + accordionDataTwo.type + '-' + accordionDataTwo.id" v-loading="accordionTwoLoading" ref="multipleTable" :data="indexResultsTable" style="width: 100%">
                            <el-table-column prop="date" label="时间"  show-overflow-tooltip header-align="center" align="center" fixed></el-table-column>
                            <el-table-column prop="loadedCount" label="已加载到JVM中类的总数"  show-overflow-tooltip header-align="center" align="center" ></el-table-column>
                            <el-table-column prop="memory" label="堆当前分配内存大小" show-overflow-tooltip header-align="center" align="center"></el-table-column>
                            <el-table-column prop="allowedSessionCount" label="允许的会话数" show-overflow-tooltip header-align="center" align="center"></el-table-column>
                            <el-table-column prop="createdSessionCount" label="会话管理器创建的会话总数" show-overflow-tooltip header-align="center" align="center"></el-table-column>
                            <el-table-column prop="activeMaxSessionCount" label="设置当前已激活会话的最大数量" show-overflow-tooltip header-align="center" align="center"></el-table-column>
                        </el-table>
  <div class="pagination-container">
                                <el-pagination
                                        @size-change="handleSizeChange"
                                        @current-change="handleCurrentChange"
                                        :current-page="currentPage"
                                        :page-size="pagesize"
                                        layout="total, sizes, prev, pager, next, jumper"
                                        :total="total">
                                </el-pagination>
                            </div>

```

```js
data 中定义的变量
data: function() {
			return {
                   currentPage:1, //初始页
                pagesize:10,    //    每页的数据　
                total:0,
                indexResultsTable:[],
                  
            }
},
// js 方法
	methods: {
             handleSizeChange:function(size){
                this.pagesize = size;
                this.getResultsTable();
            },
               handleCurrentChange:function(page){
                this.currentPage = page;
                this.getResultsTable();
            },
                //前端自己分页
              getResultsTable:function() {
                // es6过滤得到满足搜索条件的展示数据list
                var self=this;
                var list = self.accordionDataTwo.tableData;//后端回来表格的数据
                  //表格渲染的数据  indexResultsTable:[],
                this.indexResultsTable = list.filter((item, index) =>
                    index < self.currentPage * self.pagesize && index >= self.pagesize * (self.currentPage - 1)
                ) ;//根据页数显示相应的内容
                this.total = list.length;
            },
}
```

