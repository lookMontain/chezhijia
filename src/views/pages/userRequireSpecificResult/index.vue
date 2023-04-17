<template>
    <div style="padding: 20px;">
      <div class="content-box"></div>
      <div class="content-box7"></div>
      <div class="content-box8"></div>
      <div class="content-box9"></div>
      
    </div>
  </template>
  
  <script>
  
  export default {
    name: 'dashboard',
  
    data () {
  
      return {
  
      }
    },
    methods: {
      goModelComparison(){
        this.$router.push('ModelComparison')
      }
    },
    mounted () {
    }
  }
  </script>
  
  <style>
  .content-box{
    margin-top: 10px;
    height: 800px;
    background: url('../../../assets/dash-bg.png') no-repeat;
    background-size: 100%;
  }
  .content-box7{
  
    height: 800px;
    background: url('../../../assets/bg-7.png') no-repeat;
    background-size: 100%;
  }
  .content-box8{
  
  height: 800px;
  background: url('../../../assets/bg-8.png') no-repeat;
  background-size: 100%;
  }
  .content-box9{
  
  height: 800px;
  background: url('../../../assets/bg-9.png') no-repeat;
  background-size: 100%;
  }
  .bg-purple {
    background: #d3dce6;
    border-radius: 4px;
    min-height: 36px;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  </style>