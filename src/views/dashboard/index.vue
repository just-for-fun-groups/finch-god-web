<template>
  <div class="app-container">
    <el-carousel :interval="2000" type="card" height="280px" loop="true" autoplay="true">
      <el-carousel-item v-for="item in lunbo" :key="item">
        <img :src="item">
      </el-carousel-item>
    </el-carousel>
  </div>

</template>
<style>
  .el-carousel__item h3 {
    color: #475669;
    font-size: 14px;
    opacity: 0.75;
    line-height: 200px;
    margin: 0;
  }

  .el-carousel__item:nth-child(2n) {
    background-color: #99a9bf;
  }

  .el-carousel__item:nth-child(2n+1) {
    background-color: #d3dce6;
  }
</style>
<script>
  export default {
    data() {
      return {
        lunbo:[
          require("../../images/wawa.jpg"),
          require("../../images/jiaozi.jpg"),
          require("../../images/wangcai1.jpg"),
          require("../../images/wangcai2.jpg"),
          require("../../images/wangcai3.jpg"),
          require("../../images/xijiezhachuan.jpg"),

        ]
      }

    },
    methods: {
      setSize:function() {
        //设置图片大小自适应
        this.bannerHeight=400/1920*this.screenWidth;
      },
    },
    mounted(){
      this.screenWidth=window.innerWidth;
      this.setSize();
      window.onresize = ()=>{
        this.screenWidth = window.innerWidth;
        this.setSize();
      }
    }
  }
</script>
