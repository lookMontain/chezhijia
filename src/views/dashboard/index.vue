<template>
  <div style="padding: 20px;">
    <el-row :gutter="20">
      <el-col :span="8">
        <div class="grid-content bg-purple" @click="userRequierSelect">用户需求洞察</div>
      </el-col>
      <el-col :span="8">
        <div class="grid-content bg-purple">
          上市车型与专家评估
        </div>
      </el-col>
      <el-col :span="8">
        <div class="grid-content bg-purple" @click="goModelComparison">
          上市车型与消费者测评表现
        </div>
      </el-col>
    </el-row>
    <div class="content-box"></div>
    <div class="content-box7"></div>
    <div class="content-box8"></div>
    <div class="content-box9"></div>
    <el-dialog title="选择" :visible.sync="dialogVisible" width="500px" :before-close="handleClose">
      <el-row style="display: flex;justify-content: space-around;">
        <el-button type="warning">用户需求专项结论展示</el-button>
        <el-button type="danger">消费者关注度研究</el-button>
      </el-row>
    </el-dialog>
  </div>
</template>

<script>

export default {
  name: 'dashboard',

  data () {

    return {
      dialogVisible: false
    }
  },
  methods: {
    userRequierSelect () {
      this.dialogVisible = true

    },
    goModelComparison () {
      this.$router.push('ModelComparison')
    }
  },
  mounted () {
  }
}
</script>

<style>
.content-box {
  margin-top: 10px;
  height: 800px;
  background: url('../../assets/dash-bg.png') no-repeat;
  background-size: 100%;
}

.content-box7 {

  height: 800px;
  background: url('../../assets/bg-7.png') no-repeat;
  background-size: 100%;
}

.content-box8 {

  height: 800px;
  background: url('../../assets/bg-8.png') no-repeat;
  background-size: 100%;
}

.content-box9 {

  height: 800px;
  background: url('../../assets/bg-9.png') no-repeat;
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