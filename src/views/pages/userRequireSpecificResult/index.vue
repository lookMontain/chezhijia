<template>
  <div style="padding:0;" class="page-box">
    <div class="content-box-common">
      <div class="left-img-box">
        <el-image style="width: 380px; height: 380px" :src="bg1" fit="fill"></el-image>
      </div>
      <div class="right-rect">
        <div class="row-circle circle">
        </div>
        <div class="right-text-box">
          <div class="right-text-top">
            <div style="    font-size: 40px;font-weight: 800;margin-right: 10px;">儿童需求的洞察与满足</div>
            <div style="font-size: 40px;">
              <span>1</span><span>/</span><span style="color:#ff4201">2</span>
            </div>
          </div>

        </div>

      </div>
      <div class="bottom-text-box">
        <div class="text-card1" style="border-top-left-radius: 20px;">
          <div style="color:#ff8822;font-size: 20px;font-weight: 700;">场景白描</div>
          <div style="color:#969696">
            我们家小孩9岁，小朋友经常一起做车。他们一上车就是抢占三排，如果没抢到的人做二排还很委屈。会在后面看电子手表啊、玩一些小玩具什么的
          </div>
          <div style="text-align: right;display: flex;align-items: center;justify-content: flex-end;">
            <el-divider></el-divider>问界车主</div>
        </div>
        <div class="text-card1" style="margin-top: 20px;border-bottom-right-radius: 20px;">
          <div style="color:#00b5ff;font-size: 20px;font-weight: 700;">创新启迪</div>
          <div style="color:#969696">
            儿童心理学认为，这种“封闭式”的小窝，会增加儿童的安全感。可以针对三排，打造儿童专属zone，在此基础上，适当增加儿童的语音、空间交互内容等
          </div>
          <!-- <div style="text-align: right;">______问界车主</div> -->
        </div>
      </div>
    </div>
    <div class="content-box-common">
      <div class="left-img-box2">
        <el-image style="width: 380px; height: 380px" :src="bg2" fit="fill"></el-image>
      </div>
      <div class="right-rect2">
        <div class="row-circle2 circle">
        </div>
        <div class="right-text-box2">
          <div class="right-text-top">
            <div style="    font-size: 40px;font-weight: 800;margin-right: 10px;">儿童需求的洞察与满足</div>
            <div style="font-size: 40px;">
              <span>2</span><span>/</span><span style="color:#ff4201">2</span>
            </div>
          </div>

        </div>

      </div>
      <div class="bottom-text-box2">
        <div class="text-card1" style="border-top-left-radius: 20px;">
          <div style="color:#ff8822;font-size: 20px;font-weight: 700;">场景白描</div>
          <div style="color:#969696">
            我们家小孩9岁，小朋友经常一起做车。他们一上车就是抢占三排，如果没抢到的人做二排还很委屈。会在后面看电子手表啊、玩一些小玩具什么的
          </div>
          <div style="text-align: right;display: flex;align-items: center;justify-content: flex-end;">
            <el-divider></el-divider>小鹏车主</div>
        </div>
        <div class="text-card1" style="margin-top: 20px;border-bottom-right-radius: 20px;">
          <div style="color:#00b5ff;font-size: 20px;font-weight: 700;">创新启迪</div>
          <div style="color:#969696">
            儿童心理学认为，这种“封闭式”的小窝，会增加儿童的安全感。可以针对三排，打造儿童专属zone，在此基础上，适当增加儿童的语音、空间交互内容等
          </div>
          <!-- <div style="text-align: right;">______问界车主</div> -->
        </div>
      </div>
    </div>
    <div class="row4-content-box">
      <el-image style="width: 900px; height: 425px" :src="bg3" fit="fill"></el-image>
      <div class="row4-right">
        <div>
          <div style="color: #FFF;font-size: 34px;font-weight: bold;width: 400px;  margin-bottom: 20px;">
            基于家庭用车场景的座位自定义与远程调节
          </div>
          <div class="bottom-text-box3">
            <div class="text-card1" style="border-top-left-radius: 20px;  background: #242731;">
              <div style="color:#FFF;font-size: 20px;font-weight: 700;">场景白描</div>
              <div style="color:#969696">
                我昨天是二人出行，一排往后挪了很多，后备厢要放东西，三排也都放倒了。今天是四人出行，我需要一个个挪前排，还得挪二排，就很虑
              </div>
              <div style="text-align: right;display: flex;justify-content: flex-end;align-items: center;">
                <el-divider></el-divider>理想车主</div>
            </div>
            <div class="text-card1" style="margin-top: 20px;border-bottom-right-radius: 20px; background: #242731;">
              <div style="color:#FFF;font-size: 20px;font-weight: 700;">创新启迪</div>
              <div style="color:#969696">
                我们家常出行的就那么几种座位安排（比如二人模式、四人模式、带小孩模式），如果可以提前预设好，那么每次出门就可以直接选
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="content-box-common" style="    display: flex;justify-content: center;align-items: center;">
      <div class="right-rect2" style="width: 95%;">
        <div class="row-circle2 circle">
        </div>
        <div class="right-text-box2">
          <div class="right-text-top">
            <div style="font-size: 40px;font-weight: 800;margin-right: 10px;">个性化内容定制推送及</div>
          </div>
          <div style="font-size: 40px;font-weight: 800;margin-right: 10px;">
            主动智能交互
          </div>
        </div>
      </div>
      <div style="position: absolute;bottom: 20px;left: 50px;">
        <el-image style="width: 405px; height: 230px" :src="treebg" fit="fill"></el-image>
      </div>
      <div style="height: 450px;display: flex;">
        <div style="display: flex;flex-direction: column;justify-content: flex-end; margin-right: 10px;">
          <el-image style="width: 110; height: 207px" :src="center1" fit="fill"></el-image>
        </div>
        <div>
          <el-image style="width: 110; height: 207px;margin-top: 135px;" :src="center2" fit="fill"></el-image>
        </div>

      </div>
      <div style="position: absolute; right: 60px; top:120px; width: 550px;">
        <div style="font-size: 20px; font-weight: 500; margin-bottom: 16px;">Findings</div>
        <div style="color:#969696">
          现在的人生阶段处于单位中高层或私企老板，更习惯于‘听汇报’。目前的人生阶段，也让他们产生了<span style="color:#00b5ff">“掌控感”</span>。更希望车机实现<span style="color:#00b5ff">主动智能交互</span>的同时,对于车机状态,（空调）数值等信息要求：<span style="color:#00b5ff">更丰富全面,（颗粒度）更细致</span>
        </div>
      </div>
      <div style="position: absolute; right: 80px; bottom: 10px;">
        <div style="text-align: center;font-size: 16px; font-weight: 400; margin-bottom: 20px;">车辆自动检测</div>
        <el-image style="width: 420; height: 217px" :src="rightBottom" fit="fill"></el-image>
      </div>
    </div>
  </div>
</template>
  
<script>
import bg1 from '@/assets/userRequireSpecificResult/bg1.png'
import bg2 from '@/assets/userRequireSpecificResult/bg2.png'
import bg3 from '@/assets/userRequireSpecificResult/bg3.png'
import treebg from '@/assets/userRequireSpecificResult/treebg.png'
import center1 from '@/assets/userRequireSpecificResult/center1.png'
import center2 from '@/assets/userRequireSpecificResult/center2.png'
import rightBottom from '@/assets/userRequireSpecificResult/rightBottom.png'
export default {
  name: 'dashboard',

  data () {

    return {
      bg1,
      bg2,
      bg3,
      treebg,
      center1,
      center2,
      rightBottom

    }
  },
  methods: {
    goModelComparison () {
      this.$router.push('ModelComparison')
    }
  },
  mounted () {
  }
}
</script>
  
<style scoped>
.content-box-common {
  position: relative;
  background-color: #fff;
  margin: 10px 0;
  height: 500px;
  z-index: 2;
}

.left-img-box {
  height: 100%;
  width: 380px;
  display: flex;
  align-items: center;
  margin-left: 80px;

}

.right-rect {
  position: absolute;
  z-index: -1;
  right: 40px;
  top: 90px;
  width: 80%;
  height: 220px;
  border-radius: 10px;
  background: linear-gradient(to bottom, #faf9fd, #e1f5f9);

}

.row-circle {
  position: absolute;
  right: -10px;
  top: -40px;
}

.circle {
  width: 180px;
  height: 180px;
  border-radius: 50%;
  background: linear-gradient(180deg, #9cdbee, #e8e9f5);
}

.right-text-box {
  position: absolute;
  top: 20px;
  right: 70px;
}

.right-text-top {
  display: flex;
  align-items: center;
}

.bottom-text-box {
  padding: 10px;
  background-color: #f1f7fa;
  position: absolute;
  right: 20px;
  top: 190px;
  width: 600px;
  border-top-left-radius: 20px;
  border-bottom-right-radius: 20px;
  /* box-shadow: 2px 2px 2px 2px #e2ecf2; */
}

.text-card1 {
  padding-right: 50px;
  height: 120px;
  background: white;
  padding: 10px;
  display: flex;
  justify-content: space-around;
  flex-direction: column;
}

.left-img-box2 {
  position: absolute;
  right: 10px;
  height: 100%;
  width: 380px;
  display: flex;
  align-items: center;
  margin-left: 80px;
}

.right-rect2 {
  position: absolute;
  z-index: -1;
  left: 40px;
  top: 90px;
  width: 80%;
  height: 220px;
  border-radius: 10px;
  background: linear-gradient(to bottom, #faf9fd, #e1f5f9);

}

.row-circle2 {
  position: absolute;
  left: -10px;
  top: -40px;
}

.right-text-box2 {
  position: absolute;
  top: 20px;
  left: 30px;
}

.bottom-text-box2 {
  padding: 10px;
  background-color: #f1f7fa;
  position: absolute;
  left: 20px;
  top: 190px;
  width: 600px;
  border-top-left-radius: 20px;
  border-bottom-right-radius: 20px;
  /* box-shadow: 5px 0px 5px 5px #e2ecf2; */
}

.text-card1>>>.el-divider {
  padding: 0 !important;
  width: 50px;
  background: #83858a !important;
}



.row4-content-box {
  position: relative;
  height: 425px;
  background: #000;
  background-size: 100% 100%;
  display: flex;
  justify-content: flex-start;
}

.row4-right {
  position: absolute;
  right: 10px;
  bottom: 10px;
  text-align: left;
  border-radius: 5px;
  width: 600px;

  background: transparent;
  display: flex;
  align-items: center;
  color: #fff;
  margin-right: 20px;
}

.page-box>>>.el-divider {
  width: 40px !important;
  margin: 20px 0 !important;
  height: 2px !important;
  background-color: #83858a !important;
}

.row4-right-text-bottom>div {
  margin: 5px 0;
  font-size: 16px;
}

.bottom-text-box3 {
  padding: 10px;
  background: transparent;
  width: 600px;
  border-top-left-radius: 20px;
  border-bottom-right-radius: 20px;
}</style>