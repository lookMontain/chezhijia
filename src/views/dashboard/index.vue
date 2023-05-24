<template>
  <div style="padding:0;" class="page-box">
    <el-row :gutter="20" style="margin-bottom: 10px;" v-if="false">
      <el-col :span="8">
        <el-tag class="grid-content bg-purple" @click="userRequierSelect">用户需求洞察</el-tag>
      </el-col>
      <el-col :span="8">
        <el-tag type="success" class="grid-content bg-purple" @click="showMessage">
          上市车型与专家评估
        </el-tag>
      </el-col>
      <el-col :span="8">
        <el-tag type="danger" class="grid-content bg-purple" @click="goModelComparison">
          上市车型与消费者测评表现
        </el-tag>
      </el-col>
    </el-row>
    <div style="position: relative; height: 425px; background-color: #000;">
      <div class="row1-left-box">
        <div class="title-top">智能座舱</div>
        <div  style="font-size: 30px;font-weight: 400;">INTELLIGENT COCKPIT</div>
      </div>
      <el-image style="width: 899px; height: 425px" :src="url1" fit="fill"></el-image>
      <div class="row1-right-box">
        <div class="row1-right-box1" @click="goPage('ModelComparison')">
          <div class="row1-right-content-inner-box">
            <el-image  style="cursor:pointer; width: 112px%; height: 112px" :src="row1RightIcon1" fit="fill"></el-image>
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
        <div class="row1-right-box2" @click="userRequierSelect">
          <div class="row1-right-content-inner-box">
            <el-image style="cursor:pointer; width: 112px; height: 112px" :src="row1RightIcon2" fit="fill"></el-image>
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
        <div class="row1-right-box3" @click="goPage('')">
          <div class="row1-right-content-inner-box">
            <el-image style="cursor:pointer;  width: 112px%; height: 112px" :src="row1RightIcon3" fit="fill"></el-image>
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
    </div>
    <div class="row2-content-box">
      <!-- <el-image style="width: 899px; height: 425px" :src="bg2" fit="fill"></el-image> -->
      <div class="row2-left">
        <div style="margin-left: 20px;">
          <div style="color: #000;"  class="title-top">用户洞察</div>
          <el-divider></el-divider>
          <div class="title-two">
            <div>我们不只了解需求</div>
            <div>更聚焦产品的使用场景</div>
            <div>提供更为深度和科学的人群洞察观点</div>
          </div>
        </div>
      </div>
    </div>
    <div class="row3-content-box">
      <div class="row3-left">
        <el-image style="width: 380px; height: 380px" :src="row3Left" fit="fill"></el-image>
      </div>
      <div class="row3-right">
      </div>
      <div class="circle">

      </div>
      <div class="row3-right-text">
        <div   class="title-top">
          <div>我们不止</div>
          <div>
            提供基础的满意度
          </div>
        </div>
        <div class="row3-right-text-bottom title-two">
          <div>以用户整体满意度为提升目标</div>
          <div>洞察竞品横评和技术趋势</div>
          <div>输出策略性建议</div>
        </div>
      </div>
    </div>
    <div class="row4-content-box">
      <el-image style="width: 899px; height: 425px" :src="bg4" fit="fill"></el-image>
      <div class="row4-left">
        <div style="margin-left: 20px;">
          <div style="color: #FFF;" class="title-top">场景体验</div>
          <el-divider></el-divider>
          <div class="title-two">
            <div>参与并扎根中国优秀汽车的开发阶段，我们更加注重对中国消费</div>
            <div>者的洞察，提供更科学的场景洞察与测量工具模型</div>
          </div>
        </div>
      </div>
    </div>
    <div class="row5-content-box">
      <div class="row3-left">
        <el-image style="width: 380px; height: 380px" :src="row5Left" fit="fill"></el-image>
      </div>
      <div class="row3-right">
      </div>
      <div class="circle">

      </div>
      <div class="row5-right-text">
        <div class="title-top">
          <div>智驾交互</div>
        </div>
        <div style="width: 100%;display: flex;justify-content: flex-end;">
          <el-divider class="r-c-divider"></el-divider>
        </div>
        <div class="row5-right-text-bottom title-two">
          <div>利用前瞻性数据和科学分析模型</div>
          <div>帮助EMO精准定位市场</div>
          <div>科学决策产品方向,加速产品开发进度</div>
        </div>
      </div>
    </div>
    <div class="row6-content-box">
      <el-image style="width: 899px; height: 425px" :src="bg6" fit="fill"></el-image>
      <div class="row6-right">
        <div style="margin-left: 20px;">
          <div style="color: #FFF;" class="title-top">研判未来</div>
          <div style="width: 100%;display: flex;justify-content: flex-end;">
            <el-divider class="r-c-divider"></el-divider>
          </div>
          <div class="title-two" >
            <div>聚焦未来趋势研判</div>
            <div>量化需求与感知价值</div>
            <div>给出智能交互宽度和组合建议</div>
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
import row3Left from '@/assets/dashbord/row3-left.png'
import row5Left from '@/assets/dashbord/row5-left.png'
import bg4 from '@/assets/dashbord/row4-bg.png'
import bg6 from '@/assets/dashbord/row6-bg.png'
import bg2 from '@/assets/dashbord/row2-bg.png'
export default {
  name: 'dashboard',

  data () {

    return {
      dialogVisible: false,
      url1: url1,
      row1RightIcon1,
      row1RightIcon2,
      row1RightIcon3,
      row3Left,
      row5Left,
      bg6,
      bg4,
      bg2
    }
  },
  methods: {
    goPage (val) {
      if (val) {
        this.$router.push(val)
      } else {
        this.$message.info('此模块正在火速研发中，敬请期待！')
      }

    },
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

.row2-content-box {
  /* margin-top: 10px; */
  height: 425px;
  background: url('../../assets/dashbord/row2-bg.png') no-repeat;
  background-size: 100% 100%;
  display: flex;
}

.row2-left {
  border-radius: 5px;
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




.bg-purple {
  /* background: #d3dce6; */
  border-radius: 4px;
  min-height: 36px;
  display: flex;
  align-items: center;
  font-size: 20px;
  justify-content: center;
}

.row1-right-box>>>.el-divider {
  width: 40px !important;
  margin: 18px 0 !important;
}

.row2-left>>>.el-divider {
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

.row3-content-box {
  z-index: 2;
  position: relative;
  /* margin-top: 10px; */
  height: 425px;
  background: #FFF;
  /* background: url('../../assets/dashbord/row2-bg.png') no-repeat; */
  background-size: 100% 100%;
  display: flex;
}

.row3-left {
  z-index: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-left: 100px;
}

.row3-right {
  position: absolute;
  z-index: -1;
  right: 10px;
  top: 102px;
  width: 85%;
  height: 220px;
  border-radius: 10px;
  background: linear-gradient(to bottom, #faf9fd, #e1f5f9);
}

.circle {
  position: absolute;
  right: 40px;
  top: 68px;
  width: 220px;
  height: 220px;
  border-radius: 50%;
  background: linear-gradient(180deg, #9cdbee, #e8e9f5);
}

.row3-right-text {
  position: absolute;
  right: 60px;
  top: 123px;
  width: 400px;
  text-align: right;
}

.row3-right-text-top {
  font-size: 42px;
  font-weight: 800;
}

.row3-right-text-bottom {
  margin-top: 20px;
}

.row4-content-box {
  height: 425px;
  background-color: #010203;
  /* background: url('../../assets/dashbord/row4-bg3.png') repeat; */
  background-size: 100% 100%;
  display: flex;
  justify-content: flex-end;
}

.row4-left {
  left: 10px;
  position: absolute;
  border-radius: 5px;
  width: 480px;
  height: 190px;
  margin: 100px 0 0 50px;
  background: transparent;
  /* fallback for old browsers */
  /* background: -webkit-linear-gradient(to bottom right, #f8e7f6, #5bc8e5); */
  /* Chrome 10-25, Safari 5.1-6 */
  /* background: linear-gradient(to bottom right, #f8e7f6, #5bc8e5); */
  /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  display: flex;
  align-items: center;
  color: #fff;
}

.row4-left>>>.el-divider {
  width: 40px !important;
  margin: 20px 0 !important;
  background-color: #FFF !important;
}

.row5-content-box {
  z-index: 2;
  position: relative;
  /* margin-top: 10px; */
  height: 425px;
  background: #FFF;
  /* background: url('../../assets/dashbord/row2-bg.png') no-repeat; */
  background-size: 100% 100%;
  display: flex;
}

.row5-right-text {
  position: absolute;
  right: 60px;
  top: 150px;
  width: 400px;
  text-align: right;
}

.row5-right-text-bottom {
  margin-top: 20px;

}



.page-box>>>.r-c-divider {
  width: 40px;
  height: 2px !important;
  background: #01a1e6;
  margin: 10px 0 0 0 !important;
}

.row6-content-box {
  height: 425px;
  background-color: #010203;
  background-size: 100% 100%;
  display: flex;
  justify-content: space-around;
}

.row6-right {
  text-align: right;
  border-radius: 5px;
  width: 320px;
  height: 190px;
  margin: 100px 0 0 50px;
  background: transparent;
  /* fallback for old browsers */
  /* background: -webkit-linear-gradient(to bottom right, #f8e7f6, #5bc8e5); */
  /* Chrome 10-25, Safari 5.1-6 */
  /* background: linear-gradient(to bottom right, #f8e7f6, #5bc8e5); */
  /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  display: flex;
  align-items: center;
  color: #fff;
}

.row6-right>>>.el-divider {
  width: 40px !important;
  margin: 20px 0 !important;
  height: 2px !important;
  background-color: #FFF !important;
}



.bannerbox {
  width: 100%;
  position: relative;
  overflow: hidden;
  height: 500px;
}

.banner {
  width: 1920px;
  /*图片宽度*/
  position: absolute;
  left: 50%;
  margin-left: -960px;
  /*图片宽度的一半*/
}

.row1-right-content-inner-box:hover {
  width: 300px;
}

.title-top{
  font-size: 42px;
  font-weight: 800;
}
.title-two{
  font-size: 16px;
  font-weight: 400;
}
.title-two > div{
  margin: 5px 0;
}
</style>