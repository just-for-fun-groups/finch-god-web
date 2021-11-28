<template>
  <el-table
    :data="tableData"
    style="width: 100%">
    <el-table-column
      label="序号"
      prop="id">
    </el-table-column>
    <el-table-column
      label="地址"
      prop="address">
    </el-table-column>
    <el-table-column
      label="场次日期"
      prop="match_date">
    </el-table-column>
    <el-table-column label="操作">
      <template slot-scope="scope">
        <el-button
          size="mini"
          @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
        <el-button
          size="mini"
          type="danger"
          @click="handleDelete(scope.$index, scope.row)">删除</el-button>
      </template>
    </el-table-column>
  </el-table>
</template>

<style>
  .demo-table-expand {
    font-size: 0;
  }
  .demo-table-expand label {
    width: 90px;
    color: #99a9bf;
  }
  .demo-table-expand .el-form-item {
    margin-right: 0;
    margin-bottom: 0;
    width: 50%;
  }
  .el-alert__content{
    width:100%
  }
</style>

<script>
  import request from '@/utils/request';
  import axios from 'axios'

  export default {
    methods:{
      getPlayer(){
        request({
          url: '/getMatchInfo/getAllMatch',
          method: 'post',
          // data: JSON.stringify(this.form),
          baseURL: 'http://localhost:8081',
          headers:{'Content-Type': 'application/json'}
        }).then(response => {
          console.log(response);
          this.tableData=response.data;
        })
      }
    },
    created(){
      this.getPlayer();
    },
    data() {
      return {
        tableData: []
      }
    }
  }
</script>
