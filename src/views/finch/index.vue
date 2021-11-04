<template>
  <div class="app-container">
    <el-button type="text" @click="dialogFormVisible = true">新增玩家</el-button>
    <el-dialog title="玩家信息" :visible.sync="dialogFormVisible">
      <el-form :model="form">
        <el-form-item label="姓名" :label-width="formLabelWidth">
          <el-input v-model="form.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="玩家描述" :label-width="formLabelWidth">
          <el-input v-model="form.signature" autocomplete="off"></el-input>
        </el-form-item>
        <!--<el-form-item label="" :label-width="formLabelWidth">-->
        <!--<el-select v-model="form.region" placeholder="请选择活动区域">-->
        <!--<el-option label="区域一" value="shanghai"></el-option>-->
        <!--<el-option label="区域二" value="beijing"></el-option>-->
        <!--</el-select>-->
        <!--</el-form-item>-->
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="onCancel()">取 消</el-button>
        <el-button type="primary" @click="onSubmit()">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
  import request from '@/utils/request';

  export default {
    data() {
      return {
        dialogTableVisible: false,
        dialogFormVisible: false,
        form: {
          name: '',
          signature: ''
        },
        formLabelWidth: '120px'
      }
    },
    methods: {
      onSubmit() {
        request({
          url: '/getPlayerInfo/insertPlayerInfo',
          method: 'post',
          param: JSON.stringify(this.form),
          baseURL: 'http://localhost:8081'
        }).then(response => {
          console.log(response);
          this.$message('添加成功!')
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
    }
  }
</script>
