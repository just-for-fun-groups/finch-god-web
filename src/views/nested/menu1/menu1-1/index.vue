<template>
  <el-table
    :data="tableData"
    style="width: 100%"
    :row-class-name="tableRowClassName"
    v-for="{{item}}">
    <el-table-column
      prop="id"
      label="序号"
      width="100%">
    </el-table-column>
    <el-table-column
      prop="name"
      label="姓名"
      width="100%">
    </el-table-column>
    <el-table-column
      prop="signature"
      label="标志性B话"
      width="100%">
    </el-table-column>
    <el-table-column
      prop="createTime"
      label="创建时间"
      width="100%">
    </el-table-column>
    <el-table-column
      prop="updateTime"
      label="最近更改时间"
      width="100%">
    </el-table-column>
  </el-table>
</template>

<style>
  .el-table .warning-row {
    background: oldlace;
  }

  .el-table .success-row {
    background: #f0f9eb;
  }
</style>

<script>
  export default {
    methods: {
      tableRowClassName({row, rowIndex}) {
        if (rowIndex === 1) {
          return 'warning-row';
        } else if (rowIndex === 3) {
          return 'success-row';
        }
        return '';
      }
    },
    data() {
      return {
        tableData: [{
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄',
        }, {
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄',
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }]
      }
    }
  }
</script>
