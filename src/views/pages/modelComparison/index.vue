<template>
  <div style="padding: 20px;">
    <div style="display: flex;">
      <el-form size="mini" :inline="true" :model="formInline" class="demo-form-inline">
        <el-form-item label="选择车型">
          <el-select v-model="formInline.carType" placeholder="车型" multiple @change="changeType" collapse-tags>
            <el-option v-for="(item) in contrast" :key="item.name" :label="item.name" :value="item.name"></el-option>
          </el-select>
        </el-form-item>
        <!-- <el-form-item>
          <el-button type="primary" @click="onSubmit">查询</el-button>
        </el-form-item> -->
      </el-form>
      <!-- <div>
        <el-tag style="margin-right:10px ;" v-for="(item) in tags" :key="item.key" @click="scorll(item.name)">{{ item.name }}</el-tag>
      </div> -->
    </div>
    <div class="yes-sir" :style="{
      height:getHeight()+'px'
    }">
      <div class="menu-box" id="menuBox">
        <div v-for="(item, index) in tags" @click="scorll(item.label, index)" :class="{
          active: index === activeIndex
        }">
          <div>
            {{ item.label }}
          </div>
          <i class='el-icon-arrow-right'></i>
        </div>
      </div>
      <contrastCom class="contrastCom" ref='contrastCom' :contrast="showContrast" :column="column" />
    </div>

  </div>
</template>

<script>
const contrast = Object.freeze([
  {
    "name": "星越L",
    img: 1,//require('../assets/1.jpg'),
    label: '星越L',
    '氛围灯': '',
    BoomBox: '',
    '体验方向盘自定义按钮': '',
    '主题风格': '7.47',
    '灯光秀': '',
    '低速模拟声音': '',
    '相机': '7.33',
    '360全景影像监测': '7.11',
    marketTime: '2013.06',
    width_height_length: '4795*1910*1760'
  },
  {
    "name": "岚图Free",
    label: '岚图Free',
    '氛围灯': '',
    BoomBox: '',
    '体验方向盘自定义按钮': '',
    '主题风格': '7.51',
    '灯光秀': '',
    '低速模拟声音': '',
    '相册': '7.36',
    '相机': '7.73',
    '宝宝模式': "7.44",
    '行车记录仪': '7.37',
    '疲劳监测': '7.40',
    '呵护模式': '7.54',
    '照我回家': '7.46',
    marketTime: '2013.06',
    width_height_length: '4795*1910*1760'
  },
  {
    name: '小鹏P5',
    label: '小鹏P5',
    '氛围灯': '',
    BoomBox: '7.78',
    '体验方向盘自定义按钮': '',
    '主题风格': '',
    '灯光秀': '',
    '低速模拟声音': '7.65',
    '互联网浏览器': '7.81',
    '相册': '7.71',
    '相机': '7.73',
    '等人模式': '7.77',
    '360全景影像监测': '7.82',
    '充电显示': '7.87',
    '道路救援': '7.64',
    '哨兵模式': '7.84',
    '照我回家': '7.86',
    marketTime: '2013.07',
    width_height_length: '4795*1910*1760'
  },
  {
    name: 'ModelY', //require('../assets/4.jpg'),
    label: 'ModelY',
    '氛围灯': '',
    BoomBox: '7.68',
    '体验方向盘自定义按钮': '',
    '主题风格': '',
    '灯光秀': '7.62',
    '低速模拟声音': '',
    '互联网浏览器': '7.61',
    '相册': '',
    '排放测试模式': '7.51',
    '浪漫模式': '7.70',
    '代客模式': '7.66',
    '圣诞模式': '7.75',
    '行车记录仪': '7.30',
    '充电显示': '7.36',
    '能量应用程序': '7.66',
    '360全景影像监测': '',
    '道路救援': '7.16',
    '哨兵模式': '7.75',
    '爱犬模式': '7.64',
    '露营模式': '7.67',
    marketTime: '2012.06',
    width_height_length: '4795*1910*1730'
  },
  {
    name: '小鹏G9', //require('../assets/4.jpg'),
    label: '小鹏G9',
    '氛围灯': '',
    BoomBox: '',
    '体验方向盘自定义按钮': '8.22',
    '主题风格': '',
    '灯光秀': '',
    '低速模拟声音': '8.14',
    '体验办公软件': '7.40',
    '互联网浏览器': '8.40',
    '相册': '8.09',
    '相机': '7.98',
    '体验休息模式': '8.33',
    '行车记录仪': '8.32',
    '体验胎压监测': '7.95',
    '360全景影像监测': '8.10',
    '能量应用程序': '8.28',
    '道路救援': '8.18',
    '哨兵模式': '8.22',
    marketTime: '2012.06',
    width_height_length: '4795*1910*1730'
  },
  {
    name: '唐EV', //require('../assets/4.jpg'),
    label: '唐EV',
    '氛围灯': '',
    BoomBox: '',
    '体验方向盘自定义按钮': '8.04',
    '主题风格': '',
    '灯光秀': '',
    '低速模拟声音': '7.87',
    '体验办公软件': '7.68',
    '互联网浏览器': '7.71',
    '相册': '7.82',
    '相机': '7.73',
    '体验休息模式': '8.16',
    '行车记录仪': '8.00',
    '体验胎压监测': '8.26',
    '360全景影像监测': '8.00',
    '能量应用程序': '7.87',
    '道路救援': '8.00',
    '哨兵模式': '8.16',
    marketTime: '2012.06',
    width_height_length: '4795*1910*1730'
  },
  {
    name: '问卷M7', //require('../assets/4.jpg'),
    label: '问卷M7',
    '氛围灯': '',
    BoomBox: '',
    '体验方向盘自定义按钮': '8.14',
    '主题风格': '',
    '灯光秀': '',
    '低速模拟声音': '8.02',
    '体验办公软件': '7.88',
    '互联网浏览器': '7.93',
    '相册': '8.12',
    '相机': '8.12',
    '体验休息模式': '8.16',
    '行车记录仪': '8.16',
    '体验胎压监测': '8.09',
    '360全景影像监测': '8.15',
    '能量应用程序': '8.12',
    '道路救援': '8.10',
    '哨兵模式': '8.17',
    marketTime: '2012.06',
    width_height_length: '4795*1910*1730'
  },
  {
    name: '理想L9', //require('../assets/4.jpg'),
    label: '理想L9',
    '氛围灯': '',
    BoomBox: '',
    '体验方向盘自定义按钮': '8.18',
    '主题风格': '',
    '灯光秀': '',
    '低速模拟声音': '8.02',
    '体验办公软件': '8.22',
    '互联网浏览器': '8.22',
    '相册': '8.03',
    '相机': '7.99',
    '体验休息模式': '8.28',
    '行车记录仪': '8.31',
    '体验胎压监测': '8.24',
    '360全景影像监测': '8.43',
    '能量应用程序': '8.25',
    '道路救援': '8.20',
    '哨兵模式': '8.47',
    marketTime: '2012.06',
    width_height_length: '4795*1910*1730'
  }
])

const column = Object.freeze([
  // {
  //   label: '车型',
  //   prop: 'name'
  // },
  {
    label: '个性定义',
    prop: '个性定义',
    isGroup: true
  },
  {
    label: '氛围灯',
    prop: '氛围灯'
  },
  {
    label: 'BoomBox',
    prop: 'BoomBox'
  },
  {
    label: '体验方向盘自定义按钮',
    prop: '体验方向盘自定义按钮'
  },
  {
    label: '主题风格',
    prop: '主题风格'
  },
  {
    label: '灯光秀',
    prop: '灯光秀'
  }, {
    label: '低速模拟声音',
    prop: '低速模拟声音'
  },
  {
    label: '社交生活',
    prop: '社交生活',
    isGroup: true
  },
  {
    label: '体验办公软件',
    prop: '体验办公软件'
  },
  {
    label: '互联网浏览器',
    prop: '互联网浏览器'
  },
  {
    label: '相册',
    prop: '相册'
  },
  {
    label: '相机',
    prop: '相机'
  },
  {
    label: '同程订酒店',
    prop: '同程订酒店'
  },
  {
    label: '微信',
    prop: '微信'
  },
  {
    label: '安全监测',
    prop: '安全监测',
    isGroup: true
  }, {
    label: '行车记录仪',
    prop: '行车记录仪'
  },
  {
    label: '疲劳监测',
    prop: '疲劳监测'
  },
  {
    label: '体验胎压监测',
    prop: '体验胎压监测'
  },
  {
    label: '360全景影像监测',
    prop: '360全景影像监测'
  },
  {
    label: '车辆服务',
    prop: '车辆服务',
    isGroup: true
  },
  {
    label: '充电显示',
    prop: '充电显示'
  },
  {
    label: '能量应用程序',
    prop: '能量应用程序'
  },
  {
    label: '应急服务',
    prop: '应急服务',
    isGroup: true
  },
  {
    label: '道路救援',
    prop: '道路救援'
  },


  {
    label: '场景模式',
    prop: '场景模式',
    isGroup: true
  },
  {
    label: '排放测试模式',
    prop: '排放测试模式'
  },
  {
    label: '等人模式',
    prop: '等人模式'
  },
  {
    label: '浪漫模式',
    prop: '浪漫模式'
  },
  {
    label: '代客模式',
    prop: '代客模式'
  },
  {
    label: '宝宝模式',
    prop: '宝宝模式'
  },
  {
    label: '体验休息模式',
    prop: '体验休息模式'
  },

  {
    label: '圣诞模式',
    prop: '圣诞模式'
  },
  {
    label: '哨兵模式',
    prop: '哨兵模式'
  },
  {
    label: '呵护模式',
    prop: '呵护模式'
  },
  {
    label: '照我回家',
    prop: '照我回家'
  },
  {
    label: '爱犬模式',
    prop: '爱犬模式'
  },
  {
    label: '露营模式',
    prop: '露营模式'
  },
  {
    label: '驾驶成就',
    prop: '驾驶成就',
    isGroup: true
  },
  {
    label: '我的汽车',
    prop: '我的汽车',
  },
  {
    label: '车内支付',
    prop: '车内支付',
    isGroup: true
  },
  {
    label: '账单',
    prop: '账单',
  },
  {
    label: '手机APP支付',
    prop: '手机APP支付',
  },
  {
    label: '影音娱乐',
    prop: '影音娱乐',
    isGroup: true
  }, {
    label: '游戏厅',
    prop: '游戏厅',
  }, {
    label: '画板',
    prop: '画板',
  }, {
    label: '卡拉OK',
    prop: '卡拉OK',
  }, {
    label: '播放音乐',
    prop: '播放音乐',
  }, {
    label: '在线广播',
    prop: '在线广播',
  }, {
    label: '播放网络视频',
    prop: '播放网络视频',
  },


  {
    label: '车辆调节',
    prop: '车辆调节',
    isGroup: true
  }, {
    label: '开启手套箱',
    prop: '开启手套箱',
  }, {
    label: '调节遮阳帘/天幕',
    prop: '调节遮阳帘/天幕',
  }, {
    label: '车外解锁上锁反馈',
    prop: '车外解锁上锁反馈',
  }, {
    label: '座椅调节',
    prop: '座椅调节',
  }, {
    label: '控制车灯',
    prop: '控制车灯',
  }, {
    label: '调节方向盘',
    prop: '调节方向盘',
  },

  {
    label: '调节后视镜',
    prop: '调节后视镜',
  }, {
    label: '香氛开关',
    prop: '香氛开关',
  }, {
    label: '门窗锁定',
    prop: '门窗锁定',
  }, {
    label: '后备箱12V电源',
    prop: '后备箱12V电源',
  }, {
    label: '空调调节',
    prop: '空调调节',
  }, {
    label: '音频控制',
    prop: '音频控制',
  },
  {
    label: '体验后备箱调节',
    prop: '体验后备箱调节',
  },

  {
    label: '系统设置',
    prop: '系统设置',
    isGroup: true
  }, {
    label: '显示设置',
    prop: '显示设置',
  }, {
    label: '语音设置',
    prop: '语音设置',
  },
  {
    label: '用户/个人中心',
    prop: '用户/个人中心',
  },
  {
    label: '剩余流量（账户类）',
    prop: '剩余流量（账户类）',
  },
  {
    label: '云服务',
    prop: '云服务',
  }, {
    label: '拨打电话',
    prop: '拨打电话',
  },
  {
    label: '行程辅助',
    prop: '行程辅助',
    isGroup: true
  }, {
    label: '寻找附近停车位',
    prop: '寻找附近停车位',
  }, {
    label: '导航',
    prop: '导航',
  },

  {
    label: '设备互联',
    prop: '设备互联',
    isGroup: true
  }, {
    label: '智慧生活功能的操作',
    prop: '智慧生活功能的操作',
  }, {
    label: '智能召唤',
    prop: '智能召唤',
  },
  {
    label: '蓝牙手机配对',
    prop: '蓝牙手机配对',
  },
  {
    label: '寻车功能',
    prop: '寻车功能',
  },
  {
    label: '远程启动空调',
    prop: '远程启动空调',
  }, {
    label: '车载热点',
    prop: '车载热点',
  },
  {
    label: 'Wi-Fi网络连接',
    prop: 'Wi-Fi网络连接',
  },
  {
    label: 'AR眼镜功能',
    prop: 'AR眼镜功能',
  },

  {
    label: '新闻信息',
    prop: '新闻信息',
    isGroup: true
  }, {
    label: '日历/日程',
    prop: '日历/日程',
  }, {
    label: '天气和空气质量',
    prop: '天气和空气质量',
  },
  {
    label: '车辆生态',
    prop: '车辆生态',
    isGroup: true
  }, {
    label: '软件更新',
    prop: '软件更新',
  }, {
    label: '应用商店',
    prop: '应用商店',
  },

  {
    label: '驾驶辅助',
    prop: '驾驶辅助',
    isGroup: true
  }, {
    label: '驾驶辅助开关',
    prop: '驾驶辅助开关',
  }, {
    label: 'HUD抬头显示设置',
    prop: 'HUD抬头显示设置',
  },
  {
    label: '行驶信息',
    prop: '行驶信息',
  },
  {
    label: '预警提醒',
    prop: '预警提醒',
  },
  {
    label: '驾驶模式切换',
    prop: '驾驶模式切换',
  },

  {
    label: '体验悬架调节',
    prop: '体验悬架调节',
  },
  {
    label: '驾驶行为评价',
    prop: '驾驶行为评价',
  },
])

import contrastCom from './contrast'
export default {
  name: 'dashboard',
  components: { contrastCom },
  data () {

    return {
      contrast, // 对比数据，与平时使用相同
      column,// 左侧名称和顺序
      formInline: {
        carType: []
      },

      showContrast: [],
      tags: [],
      activeIndex: 0
    }
  },
  methods: {
    getHeight () {
      const innerHeight = window.innerHeight
      return innerHeight - 150
    },
    initTags () {

      this.tags = this.column.filter(item => item.isGroup)
    },
    initShowContrast () {
      this.formInline.carType = this.contrast.slice(0, 6).map(item => item.name)
      this.showContrast = this.contrast.slice(0, 6)
    },
    scorll (id, index) {
      this.activeIndex = index
      this.$refs.contrastCom.scorll(id, index)
    },
    changeType (value) {
      const list = this.contrast.filter(item => value.includes(item.name))
      this.showContrast = list
    },
    getScrollTo (id, i) {
      var element = document.getElementById('box');
      let offsetTop = document.querySelector(`#${id}`).offsetTop;
      element.scrollTop = offsetTop - (i * 40);
    },
    scrollIntoView (id) {
      var element = document.getElementById(id);
      element.scrollIntoView();
      //element.scrollIntoView({behavior: "instant", block: "end", inline: "nearest"});
    },
  },
  mounted () {
    this.initTags()
    this.initShowContrast()
  }
}
</script>

<style scoped>
.box {
  /* display: flex;  calc(100vh - 180px); */
  overflow-y: scroll;
  padding: 10px;
  flex: 1;
  height: calc(100vh - 180px);
  padding-bottom: 500px;
}

.tableHead {
  width: 300px;
  float: left;
  color: #386ed3;
}

.tableBody {
  display: flex;
  overflow-x: scroll;
  /* float: left; */
}

.singleRow {
  width: 180px;
}

.el-row {
  margin: 0px -1px -1px -1px;
  /*解决边框重叠*/
  text-align: center;
  font-size: 14px;
  line-height: 42px;
  border: 1px solid #e6e6e6;
}

.column {
  border: 1px solid #e6e6e6;
  /* height: 43px; */
  border-top: none;
  border-left: none;
}

.otherCol {
  height: 43px;
}

.nameCol {
  height: 120px;
}

.name-bottom {
  color: rgb(255, 131, 0);
  display: flex;
  justify-content: space-around;
  margin-top: 20px;
}

.secondLevelClass {
  background-color: #f8f8f8;
  text-align: left;
  color: #4A4A4A;
  font-weight: bold;
}


.menu-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 10px 0;
  cursor: pointer;
}

.menu-item:hover {
  background-color: #409eff;
  font-size: 18px;
  color: #fff;
}

.content-box {
  display: flex;
  overflow-y: scroll;
  padding: 10px;
  /* height: calc(100vh - 130px); */
}

.row-box {
  display: flex;
  border: 1px solid #e5e5e5;

  height: 40px;
  line-height: 40px;

}

.row-item {
  width: 160px;
  border-right: 1px solid #e5e5e5
}

.row1-1 {
  height: 50px;
  background: #e4e4e4;
  line-height: 50px;
}

.container-box {
  display: flex;
  flex-direction: column;
}

.container-detail {
  height: 500px;
  overflow-y: scroll
}

.row1Style {
  height: 130px;
  background: #f8f8f8;
}

.row1-item {
  height: 100%;
  display: flex;
  justify-content: center;
  flex-direction: column;
}

.row1-item>div {
  text-align: center;
}

.row1-title1 {
  font-size: 20px;
  font-weight: 800;
}

.row1-title2 {
  color: #ff9600;
  margin: 5px 0;
}

.row1itemStyle {
  line-height: 130px;
  text-align: center;
}

.content {
  width: 100%;
}

.yes-sir {
  width: 100%;
  display: flex;
  margin: 10px auto;
  border: solid 1px #eee;
}

.menu-box {
  width: 140px;
  padding-top: 60px;
  overflow-y: scroll;
}

.menu-box>div {
  height: 43px;
  display: flex;
  background: #d6d6d6;
  align-items: center;
  margin-bottom: 1px;
  justify-content: space-around;

}

.menu-box>div:hover {
  background-color: #ecf5ff;

}

.contrastCom {
  min-width: 0;
}

.active {
  color: #fff;
  background-color: #67c23a !important;
  border-color: #67c23a;
}
</style>
