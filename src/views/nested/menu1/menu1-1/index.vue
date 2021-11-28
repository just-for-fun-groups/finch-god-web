<template>
  <div class="app-container">
    <el-button type="primary" @click="dialogFormVisible = true">新增玩家</el-button>
    <el-dialog title="玩家信息" :visible.sync="dialogFormVisible">
      <el-form :model="form">
        <el-form-item label="姓名" :label-width="formLabelWidth">
          <el-input v-model="form.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="玩家描述" :label-width="formLabelWidth">
          <el-input v-model="form.signature" autocomplete="off"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="onCancel()">取 消</el-button>
        <el-button type="primary" @click="onSubmit()">确 定</el-button>
      </div>
    </el-dialog>

    <el-table
      :data="tableData"
      style="width: 100%">
      <el-table-column type="expand">
        <template slot-scope="props">
          <el-form label-position="left" inline class="demo-table-expand">
            <el-form-item label="商品名称">
              <span>{{ props.row.name }}</span>
            </el-form-item>
            <el-form-item label="所属店铺">
              <span>{{ props.row.shop }}</span>
            </el-form-item>
            <el-form-item label="商品 ID">
              <span>{{ props.row.id }}</span>
            </el-form-item>
            <el-form-item label="店铺 ID">
              <span>{{ props.row.shopId }}</span>
            </el-form-item>
            <el-form-item label="商品分类">
              <span>{{ props.row.category }}</span>
            </el-form-item>
            <el-form-item label="店铺地址">
              <span>{{ props.row.address }}</span>
            </el-form-item>
            <el-form-item label="商品描述">
              <span>{{ props.row.desc }}</span>
            </el-form-item>
          </el-form>
        </template>
      </el-table-column>
      <el-table-column
        label="序号"
        prop="id">
      </el-table-column>
      <el-table-column
        label="姓名"
        prop="name">
      </el-table-column>
      <el-table-column
        label="B话"
        prop="signature">
      </el-table-column>
      <el-table-column label="操作">
        <template slot-scope="scope">
          <el-button
            size="mini"
            type="danger"
            @click="handleDelete(scope.$index, scope.row)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
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
    width: 100%;
  }
</style>

<script>
  import request from '@/utils/request';
  import axios from 'axios'

  export default {
    methods:{
      getPlayer(){
        request({
          url: '/getPlayerInfo/getAllPlayer',
          method: 'post',
          // data: JSON.stringify(this.form),
          baseURL: 'http://localhost:8081',
          headers:{'Content-Type': 'application/json'}
        }).then(response => {
          console.log(response);
          this.tableData=response.data;
        })
      },
      //编辑
      handleEdit(){

      },
      //删除
      handleDelete(index,row){
        var confim = window.confirm("确认删除该玩家吗?");
        if (confim){
          request({
            url: '/getPlayerInfo/deletePlayerInfo',
            method: 'post',
            data: JSON.stringify(row),
            baseURL: 'http://localhost:8081',
            headers:{'Content-Type': 'application/json'}
          }).then(response => {
            console.log(response);
            this.$message('删除成功!');
            this.getPlayer();
          })
        }
      },
      onSubmit() {
        request({
          url: '/getPlayerInfo/insertPlayerInfo',
          method: 'post',
          data: JSON.stringify(this.form),
          baseURL: 'http://localhost:8081',
          headers:{'Content-Type': 'application/json'}
        }).then(response => {
          console.log(response);
          this.$message('添加成功!');
          this.getPlayer();
        })
        this.$message('submit!')
        this.dialogFormVisible = false
        this.dialogTableVisible = false
      },
      onCancel() {
        this.dialogFormVisible = false
        this.dialogTableVisible = false
        this.$message({
          message: 'cancel!',
          type: 'warning'
        })
      }
    },
    created(){
      this.getPlayer();
    },
    data() {
      return {
        tableData: [],
        dialogTableVisible: false,
        dialogFormVisible: false,
        form: {
          name: '',
          signature: ''
        },
        formLabelWidth: '120px'
      }
    }
  }
</script>
