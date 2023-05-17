<template>
  <div style="padding: 20px;">
    <el-row :gutter="20">
      <el-col :span="8">
        <div class="grid-content bg-purple" @click="userRequierSelect">用户需求洞察</div>
      </el-col>
      <el-col :span="8">
        <div class="grid-content bg-purple" @click="showMessage">
          上市车型与专家评估
        </div>
      </el-col>
      <el-col :span="8">
        <div class="grid-content bg-purple" @click="goModelComparison">
          上市车型与消费者测评表现
        </div>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="24" style="position: relative;">
        <div class="row1-left-box">
          <div style="font-size: 50px;font-weight: 500;">智能座舱</div>
          <div style="font-size: 30px;font-weight: 300;">INTELLIGENT COCKPIT</div>
        </div>
        <el-image style="width: 100%; height: 425px" :src="url1" fit="fill"></el-image>

        <div class="row1-right-box">
          <div class="row1-right-box1">
            <div class="row1-right-content-inner-box">
              <el-image style="width: 112px%; height: 112px" :src="row1RightIcon1" fit="fill"></el-image>
              <div class="row1-right-box-title1">
                竞品表现
              </div>
              <el-divider></el-divider>
              <div class="row1-right-box-buttom">
                <div class="item-title">
                  功能评估
                </div>
                <div class="item-title">
                  亮点评估
                </div>
              </div>
            </div>
          </div>
          <div class="row1-right-box2">
            <div class="row1-right-content-inner-box">
              <el-image style="width: 112px%; height: 112px" :src="row1RightIcon2" fit="fill"></el-image>
              <div class="row1-right-box-title1">
                用户需求
              </div>
              <el-divider></el-divider>
              <div class="row2-right-box-buttom">
                <div class="item-title">
                  用车场景
                </div>
                <div class="item-title">
                  现有需求
                </div>
                <div class="item-title">
                  需求趋势
                </div>
              </div>
            </div>
          </div>
          <div class="row1-right-box3">
            <div class="row1-right-content-inner-box">
              <el-image style="width: 112px%; height: 112px" :src="row1RightIcon3" fit="fill"></el-image>
              <div class="row1-right-box-title1">
                专家评审
              </div>
              <el-divider></el-divider>
              <div class="row3-right-box-buttom">
                <div class="item-title">
                  技术趋势
                </div>
                <div class="item-title">
                  技术评估
                </div>
                <div class="item-title">
                  深度评价
                </div>
              </div>
            </div>

          </div>
        </div>
      </el-col>

    </el-row>
    <div class="content-box">
      <div class="row2-left">
        <div style="margin-left: 20px;">
          <div style="color: #000;font-size: 24px;font-weight: bold;">用户洞察</div>
          <el-divider></el-divider>
          <div>
            <div>我们不只了解需求</div>
            <div>更聚焦产品的使用场景</div>
            <div>提供更为深度和科学的人群洞察观点</div>
          </div>
        </div>
      </div>
    </div>
    <el-dialog title="选择" :visible.sync="dialogVisible" width="500px">
      <el-row style="display: flex;justify-content: space-around;">
        <el-button type="warning" @click="goUserRequireSpecificResult">用户需求专项结论展示</el-button>
        <el-button type="danger" @click="showMessage">消费者关注度研究</el-button>
      </el-row>
    </el-dialog>
  </div>
</template>

<script>
import url1 from '@/assets/dashbord/url1.png'
import row1RightIcon1 from '@/assets/dashbord/row1-right-item1-icon.png'
import row1RightIcon2 from '@/assets/dashbord/row1-right-item2-icon.png'
import row1RightIcon3 from '@/assets/dashbord/row1-right-item3-icon.png'

export default {
  name: 'dashboard',

  data () {

    return {
      dialogVisible: false,
      url1: url1,
      row1RightIcon1,
      row1RightIcon2,
      row1RightIcon3
    }
  },
  methods: {
    userRequierSelect () {
      this.dialogVisible = true

    },
    goUserRequireSpecificResult () {
      this.$router.push('UserRequireSpecificResult')
    },
    goModelComparison () {
      this.$router.push('ModelComparison')
    },
    showMessage () {
      this.$message.info('此模块正在火速研发中，敬请期待！')
    }
  },
  mounted () {
  }
}
</script>

<style scoped>
.row1-right-box {
  position: absolute;
  top: 0;
  width: 50%;
  right: 0;
  height: 100%;
  display: flex;
  color: #FFF;
}

.row1-right-box1 {
  flex: 1;
  height: 99%;
  /* width: 33.3%; */
  background: url(../../assets/dashbord/row1-right-item1.png) no-repeat;
  background-size: 100% 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.row1-right-box2 {
  flex: 1;
  height: 99%;
  /* width: 33.3%; */
  background: url(../../assets/dashbord/row1-right-item2.png) no-repeat;
  background-size: 100% 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.row1-right-box3 {
  flex: 1;
  height: 99%;
  /* width: 33.3%; */
  background: url(../../assets/dashbord/row1-right-item3.png) no-repeat;
  background-size: 100% 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.row1-right-content-inner-box {
  height: 300px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.content-box {
  margin-top: 10px;
  height: 425px;

  background: url('../../assets/dashbord/row2-bg.png') no-repeat;
  background-size: 100% 100%;
  display: flex;
}

.row2-left {
  width: 350px;
  height: 190px;
  margin: 100px 0 0 50px;
  background: #00fff0;
  /* fallback for old browsers */
  background: -webkit-linear-gradient(to bottom right, #f8e7f6, #5bc8e5);
  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to bottom right, #f8e7f6, #5bc8e5);
  /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  display: flex;
    align-items: center;

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

.row1-right-box>>>.el-divider {
  width: 40px !important;
  margin: 18px 0 !important;
}
.row2-left >>> .el-divider {
  width: 40px !important;
  margin: 10px 0 !important;
  background-color: #244082 !important;
}

.row1-right-box-title1 {
  font-size: 24px;
  margin: 20px 0 10px 0;
}

.row1-right-box-buttom {
  font-size: 18px;
  height: 100px;
  width: 155px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: url(../../assets/dashbord/row1-right-item1-icon2.png) no-repeat;
  background-size: 100% 100%;
}

.row2-right-box-buttom {
  font-size: 18px;
  height: 100px;
  width: 155px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: url(../../assets/dashbord/row1-right-item2-icon2.png) no-repeat;
  background-size: 100% 100%;
}

.row3-right-box-buttom {
  font-size: 18px;
  height: 100px;
  width: 155px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: url(../../assets/dashbord/row1-right-item3-icon2.png) no-repeat;
  background-size: 100% 100%;
}

.row1-left-box {
  position: absolute;
  color: #ffffff;
  left: 50px;
  top: 50px;
  /* width: 100px; */
  z-index: 999;
}

.row1-right-box .item-title {
  margin: 2px 0;
}

</style>