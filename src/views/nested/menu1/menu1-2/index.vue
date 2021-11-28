<template>
  <div class="app-container">
    <el-button type="primary" @click="dialogFormVisible = true">新增比赛</el-button>
    <el-dialog title="比赛信息" :visible.sync="dialogFormVisible">
      <el-form :model="form">
        <el-form-item label="比赛地址" :label-width="formLabelWidth" >
          <el-select v-model="addressValue" filterable placeholder="请选择" clearable=true no-match-text="无匹配">
            <el-option
              v-for="item in addressOptions"
              :key="item.id"
              :label="item.address"
              :value="item.id">
            </el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="玩家" :label-width="formLabelWidth">
          <el-button type="primary" @click="addressFormVisible = true">添加玩家</el-button>
          <el-dialog title="玩家信息" :visible.sync="addressFormVisible">
            <el-form :model="form">
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
                  label="玩家"
                  prop="players">
                </el-table-column>
                <el-table-column
                  label="场次日期"
                  prop="match_date">
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
            </el-form>
          </el-dialog>
        </el-form-item>
        <el-form-item label="比赛日期" :label-width="formLabelWidth">
          <el-date-picker
            v-model="value1"
            type="datetime"
            placeholder="选择日期时间">
          </el-date-picker>
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
        label="玩家"
        prop="players">
      </el-table-column>
      <el-table-column
        label="场次日期"
        prop="match_date">
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
    width:100%
  }
</style>

<script>
  import request from '@/utils/request';
  import axios from 'axios'

  export default {
    methods:{
      getMatch(){
        request({
          url: '/getMatchInfo/getAllMatch',
          method: 'post',
          // data: JSON.stringify(this.form),
          baseURL: 'http://localhost:8081',
          headers:{'Content-Type': 'application/json'}
        }).then(response => {
          console.log(response);
          this.tableData=response.data;
          this.addressOptions = response.data;
        })
      },
      getMatchAddress(){
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
      this.getMatch();
      //
    },
    data() {
      return {
        value1: '',
        tableData: [],
        addressOptions:[],
        playerOption:[],
        addressValue:'',
        addressFormVisible:false,
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
