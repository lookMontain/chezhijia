<template>
  <el-container style="background: #fff;">
    <el-main>
      <div>
        <div style="display: flex; flex-direction: column;">
          <div class="tip-box">
            <div> <i style="color:#fdab00" class="el-icon-message-solid"></i> 温馨提示：请添加筛选条件查询相关内容</div>
            <div><i style="color:#000" class="el-icon-close"></i></div>
          </div>
          <el-form size="mini" :inline="true" :model="formInline" class="demo-form-inline">
            <el-form-item label="价位">
              <el-select clearable v-model="formInline.price" multiple @change="onSubmit" placeholder="请选择" collapse-tags>
                <el-option v-for="(item) in priceOptions" :key="item.value" :label="item.label"
                  :value="item.value"></el-option>
              </el-select>
            </el-form-item>
            <el-form-item label="细分市场">
              <el-select clearable v-model="formInline.market" multiple @change="onSubmit" placeholder="请选择"
                collapse-tags>
                <el-option v-for="(item) in marketOptions" :key="item.value" :label="item.label"
                  :value="item.value"></el-option>
              </el-select>
            </el-form-item>
            <el-form-item label="品牌">
              <el-select clearable v-model="formInline.brand" multiple @change="onSubmit" placeholder="请选择" collapse-tags>
                <el-option v-for="(item) in brandOptions" :key="item.value" :label="item.label"
                  :value="item.value"></el-option>
              </el-select>
            </el-form-item>

            <el-form-item>
              <el-button type="primary" @click="onSubmit">查询</el-button>
              <el-button @click="resetForm()">重置</el-button>
            </el-form-item>
          </el-form>
          <div></div>
          <el-form size="mini" :inline="true" :model="formInline" class="demo-form-inline">
            <el-form-item label="车型">
              <el-select v-model="formInline.carType" placeholder="请选择" multiple @change="changeType" collapse-tags>
                <el-option v-for="(item) in contrastOption" :key="item.name" :label="item.name"
                  :value="item.name"></el-option>
              </el-select>
            </el-form-item>
          </el-form>
          <div style="position: absolute;right: 50px;top: 80px;">
            <el-popover placement="bottom-start" title="数据说明" width="300" trigger="hover">
              <div>
                <br/>
                <span style="color:red">1</span>.本页数据为：交互功能体验满意度数据，即用户操作某项功能时的交互体验满意度；
                <br/>
                <br/>
                <span style="color:red">2</span>.交互体验满意度包含6个评价维度，分别为：功能丰富、逻辑合理、交互便捷、视觉美观、功能可靠、使用安全；
                <br/>
                <br/>
                <span style="color:red">3</span>.交互体验满意度的评价，来源于同级别细分市场用户；
              </div>
              <i slot="reference" class="el-icon-warning" style="color:#fdab00;font-size: 20px;"></i>
            </el-popover>
          </div>
        </div>
        <div v-if='formInline.carType.length' class="yes-sir" :style="{
          height: getHeight() + 'px'
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
        <div class="empty" v-else :style="{
          height: getHeight() + 'px'
        }">
          <el-image style="width: 251px; height: 259px" :src="empty" fit="fill"></el-image>
        </div>

      </div>
    </el-main>
  </el-container>
</template>

<script>
import allData from '../mock/all.json'
import empty from '@/assets/empty.png'
const contrast1 = Object.freeze([
  {
    "name": "星越L",
    label: '星越L',
    '氛围灯': '',
    BoomBox: '',
    '体验方向盘自定义按钮': '',
    '主题风格': '7.47',
    '灯光秀': '',
    '低速模拟声音': '',
    '相机': '7.33',
    '360全景影像监测': '7.11',
    '我的汽车': '7.57',
    '调节遮阳帘/天幕': '7.34',
    '座椅调节': '7.72',
    '控制车灯': "7.60",
    '调节方向盘': '7.47',
    '空调调节': '7.31',
    '音频控制': '7.29',
    '微信': '7.30',
    '显示设置': '7.26',
    '语音设置': '7.44',
    '导航': '7.38',
    '卡拉OK': '7.10',
    '播放音乐': '7.47',
    '在线广播': '7.16',
    '播放网络视频': '7.11',
    '智能召唤': "7.63",
    '蓝牙手机配对': '7.01',
    '远程启动空调': 7.66,
    '车载热点': 7.60,
    'Wi-Fi网络连接': 7.54,
    '用户/个人中心': 7.36,
    '同程订酒店': 6.84,
    '日历/日程': 6.77,
    '天气和空气质量': 6.83,
    '应用商店': 7.53,
    '拨打电话': 7.08,
    '驾驶辅助开关': 6.91,
    'HUD抬头显示设置': 7.39,
    '行驶信息': 6.97,
    '预警提醒': 6.77,
    '驾驶模式切换': 6.75
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
    '账单': '7.42',
    '手机APP支付': '7.46',
    '调节遮阳帘/天幕': '7.62',
    '座椅调节': '7.61',
    '控制车灯': "7.49",
    '调节后视镜': '7.44',
    '香氛开关': '7.51',
    '门窗锁定': '7.43',
    '空调调节': '7.51',
    '音频控制': '7.42',
    '显示设置': '7.33',
    '语音设置': '7.37',
    '寻找附近停车位': '7.30',
    '导航': '7.51',
    '卡拉OK': '7.31',
    '播放音乐': '7.49',
    '在线广播': '7.27',
    '播放网络视频': '7.42',
    '蓝牙手机配对': '7.37',
    '远程启动空调': 7.57,
    '车载热点': 7.39,
    'Wi-Fi网络连接': 7.39,
    '用户/个人中心': 7.33,
    '剩余流量（账户类）': 7.35,
    '同程订酒店': 7.41,
    '日历/日程': 7.08,
    '软件更新': 7.45,
    '拨打电话': 7.34,
    '驾驶辅助开关': 7.43,
    '行驶信息': 7.56,
    '预警提醒': 7.46,
    '驾驶模式切换': 7.46
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
    '账单': '7.71',
    '手机APP支付': '7.68',
    '游戏厅': '7.57',
    '调节遮阳帘/天幕': '7.82',
    '车外解锁上锁反馈': '7.80',
    '座椅调节': '7.80',
    '控制车灯': "7.71",
    '调节方向盘': '7.71',
    '调节后视镜': '7.73',
    '香氛开关': '7.81',
    '门窗锁定': '7.75',
    '后备箱12V电源': '7.80',
    '空调调节': '7.85',
    '音频控制': '7.87',
    '显示设置': '7.77',
    '语音设置': '7.69',
    '导航': '7.93',
    '卡拉OK': '7.69',
    '播放音乐': '7.90',
    '在线广播': '7.81',
    '播放网络视频': '7.85',
    '蓝牙手机配对': '7.88',
    '远程启动空调': 7.83,
    'Wi-Fi网络连接': 7.73,
    '用户/个人中心': 7.56,
    '剩余流量（账户类）': 7.61,
    '云服务': 7.57,
    '软件更新': 7.82,
    '应用商店': 7.79,
    '拨打电话': 7.87,
    '驾驶辅助开关': 7.82,
    '行驶信息': 7.85,
    '预警提醒': 7.84,
    '驾驶模式切换': 7.88
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
    '手机APP支付': '7.69',
    '游戏厅': '7.78',
    '画板': '7.60',
    '开启手套箱': '7.47',
    '控制车灯': "7.60",
    '调节方向盘': '7.73',
    '调节后视镜': '7.63',
    '门窗锁定': '7.62',
    '空调调节': '7.53',
    '音频控制': '7.51',
    '显示设置': '7.42',
    '导航': '7.47',
    '卡拉OK': '7.16',
    '播放音乐': '7.53',
    '在线广播': '7.24',
    '播放网络视频': '7.27',
    '智能召唤:': '7.66',
    '蓝牙手机配对': 7.46,
    '远程启动空调': 7.73,
    'Wi-Fi网络连接': 7.59,
    '用户/个人中心': 7.58,
    '日历/日程': 7.25,
    '天气和空气质量': 7.41,
    '软件更新': 7.67,
    '拨打电话': 7.13,
    '驾驶辅助开关': 7.34,
    '行驶信息': 7.39,
    '预警提醒': 7.34,
    '驾驶模式切换': 7.33
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
    '游戏厅': '7.95',
    '香氛开关': '7.26',
    '门窗锁定': '8.41',
    '体验后备箱调节': '8.31',
    '微信': '8.00',
    '显示设置': '8.23',
    '语音设置': '8.20',
    '导航': '8.27',
    '卡拉OK': '8.14',
    '播放音乐': '8.34',
    '在线广播': '8.17',
    '播放网络视频': '8.33',
    '智慧生活功能的操作': '8.36',
    '蓝牙手机配对': 8.16,
    '寻车功能': 8.31,
    '远程启动空调': 8.32,
    'AR眼镜功能': 8.40,
    '用户/个人中心': 8.17,
    '日历/日程': 7.89,
    '天气和空气质量': 7.97,
    '应用商店': 8.17,
    '拨打电话': 8.14,
    '行驶信息': 8.16,
    '驾驶模式切换': 8.21,
    '体验悬架调节': 8.12
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
    '游戏厅': '7.72',
    '香氛开关': '8.07',
    '门窗锁定': '7.76',
    '体验后备箱调节': '7.76',
    '微信': '8.01',
    '显示设置': '7.71',
    '语音设置': '7.81',
    '导航': '7.99',
    '卡拉OK': '7.87',
    '播放音乐': '7.99',
    '在线广播': '7.88',
    '播放网络视频': '8.06',
    '智慧生活功能的操作': '8.22',
    '蓝牙手机配对': 8.03,
    '寻车功能': 8.01,
    '远程启动空调': 8.03,
    'AR眼镜功能': 8.17,
    '用户/个人中心': 7.75,
    '日历/日程': 7.69,
    '天气和空气质量': 8.01,
    '应用商店': 7.99,
    '拨打电话': 8.00,
    '行驶信息': 7.84,
    '驾驶模式切换': 8.04,
    '体验悬架调节': 8.04
  },
  {
    name: '问界M7', //require('../assets/4.jpg'),
    label: '问界M7',
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
    '游戏厅': '7.93',
    '香氛开关': '7.99',
    '门窗锁定': '8.02',
    '体验后备箱调节': '8.05',
    '微信': '8.18',
    '显示设置': '8.25',
    '语音设置': '8.17',
    '导航': '8.22',
    '卡拉OK': '7.81',
    '播放音乐': '8.11',
    '在线广播': '8.15',
    '播放网络视频': '8.06',
    '智慧生活功能的操作': '8.23',
    '蓝牙手机配对': 8.26,
    '寻车功能': 8.25,
    '远程启动空调': 8.28,
    'AR眼镜功能': 8.17,
    '用户/个人中心': 7.97,
    '日历/日程': 8.23,
    '天气和空气质量': 8.25,
    '应用商店': 8.19,
    '拨打电话': 8.21,
    '行驶信息': 8.13,
    '驾驶模式切换': 8.22,
    '体验悬架调节': 8.25
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
    '我的汽车': '',
    '游戏厅': '8.22',
    '香氛开关': '8.16',
    '门窗锁定': '8.30',
    '体验后备箱调节': '8.34',
    '微信': '8.24',
    '显示设置': '8.27',
    '语音设置': '8.30',
    '导航': '8.41',
    '卡拉OK': '8.29',
    '播放音乐': '8.47',
    '在线广播': '8.12',
    '播放网络视频': '8.43',
    '智慧生活功能的操作': '8.39',
    '蓝牙手机配对': 8.23,
    '寻车功能': 8.32,
    '远程启动空调': 8.30,
    'AR眼镜功能': 8.20,
    '用户/个人中心': 8.17,
    '日历/日程': 8.04,
    '天气和空气质量': 8.36,
    '应用商店': 8.17,
    '拨打电话': 8.36,
    '行驶信息': 8.14,
    '驾驶模式切换': 8.29,
    '体验悬架调节': 8.26
  }
])
const contrast = Object.freeze(allData)

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
    isGroup: true,
    order: 3,
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
    isGroup: true,
    order: 1,

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
    isGroup: true,
    order: 2
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
    isGroup: true,
    order: 4
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
    isGroup: true,
    order: 5
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
      empty,
      contrast, // 对比数据，与平时使用相同
      column,// 左侧名称和顺序
      formInline: {
        carType: [],
        price: [],
        market: [],
        brand: []
      },

      showContrast: [],
      tags: [],
      activeIndex: 0,
      priceOptions: [{
        value: "10-20",
        label: '10万-20万'
      }, {
        value: "20-30",
        label: '20万-30万'
      }, {
        value: "30-40",
        label: '30万-40万'
      }],
      marketOptions: [{
        value: "紧凑型SUV",
        label: "紧凑型SUV"
      }, {
        value: "中型SUV",
        label: "中型SUV"
      }, {
        value: "中大型SUV",
        label: "中大型SUV"
      }, {
        value: "紧凑型轿车",
        label: "紧凑型轿车"
      }],
      brandOptions: [{
        value: "理想",
        label: "理想"
      }, {
        value: "问界",
        label: "问界"
      }, {
        value: "比亚迪",
        label: "比亚迪"
      }, {
        value: "小鹏",
        label: "小鹏"
      }, {
        value: "特斯拉",
        label: "特斯拉"
      }, {
        value: "岚图",
        label: "岚图"
      }, {
        value: "吉利",
        label: "吉利"
      }],
      contrastOption: []
    }
  },
  methods: {
    resetForm () {
      this.formInline.price = []
      this.formInline.market = []
      this.formInline.brand = []
      this.formInline.carType = []
      this.contrastOption = this.contrast
      this.showContrast = []
      // 重新获取车型
    },
    // 根据条件查车型
    onSubmit () {
      const { price, market, brand } = this.formInline
      const list = this.contrast.filter(item => {
        let isOk = true
        if (price && price.length) {
          const target = price.find(xitem => {
            const range = xitem.split('-')
            if (item.price >= range[0] && item.price <= range[1]) {
              return item
            }
          })
          if (!target) {
            isOk = false
          }
        }
        if (market && market.length) {
          if (!market.find(x => x === item.market)) {
            isOk = false
          }
        }
        if (brand && brand.length) {
          if (!brand.find(x => x === item.brand)) {
            isOk = false
          }
        }
        return isOk
      })
      this.contrastOption = list
      // 把list中的name筛选出来， 如果carType 中存在则保留，不存在把carType中的剔除
      const nameList = list.map(item => item.name)
      this.formInline.carType = this.formInline.carType.filter(item => nameList.includes(item))
      this.showContrast = this.showContrast.filter(item => nameList.includes(item.name))
    },
    getHeight () {
      const innerHeight = window.innerHeight
      return innerHeight - 230
    },
    initTags () {
      this.column.forEach(item => {
        if (!item.order) {
          item.order = 9000
        }
      })
      this.tags = this.column.filter(item => item.isGroup).sort((val1, val2) => {
        return val1.order - val2.order
      });
      setTimeout(() => {
        this.$nextTick(() => {
          this.scorll('车辆调节', 0)
        })
      })

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
    this.contrastOption = this.contrast
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
  /* padding-top: 60px; */
  overflow-y: scroll;
}

.menu-box>div {
  height: 48px;
  display: flex;
  /* background: #d6d6d6; */
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

.tip-box {
  background: #e9f8ff;
  display: flex;
  justify-content: space-between;
  height: 36px;
  align-items: center;
  padding: 0 10px;
  border-radius: 6px;
  border: 1px solid #67b0ee;
  margin: 0 20px 10px 20px;
  color: #3da6e4;
  font-size: 10px;
  font-weight: 500;
}

/*定义滚动条高宽及背景
 高宽分别对应横竖滚动条的尺寸*/
.menu-box::-webkit-scrollbar {
  width: 8px;
  height: 8px;
  background-color: #fff;
}

/*定义滚动条轨道
 内阴影+圆角*/
.menu-box::-webkit-scrollbar-track {
  -webkit-box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.3);
  border-radius: 10px;
  background-color: #FFF;
}

/*定义滑块
     内阴影+圆角*/
.menu-box::-webkit-scrollbar-thumb {
  border-radius: 10px;
  width: 4px;
  height: 4px;
  -webkit-box-shadow: inset 0 0 6px rgba(0, 0, 0, .3);
  background-color: #c6d5dc;
}

.empty {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
