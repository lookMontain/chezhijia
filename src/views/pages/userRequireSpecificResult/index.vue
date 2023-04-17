<template>
    <div style="padding: 20px;">
      <div class="content-box1"></div>
      <div class="content-box2"></div>
      <div class="content-box3"></div>
      <div class="content-box4"></div>
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
  .content-box1{
    margin-top: 10px;
    height: 800px;
    background: url('../../../assets/bg-e1.png') no-repeat;
    background-size: 100%;
  }
  .content-box2{
  
    height: 800px;
    background: url('../../../assets/bg-e2.png') no-repeat;
    background-size: 100%;
  }
  .content-box3{
  
  height: 800px;
  background: url('../../../assets/bg-e3.png') no-repeat;
  background-size: 100%;
  }
  .content-box4{
  
  height: 800px;
  background: url('../../../assets/bg-e4.png') no-repeat;
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