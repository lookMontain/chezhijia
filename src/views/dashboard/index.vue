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
      <div>
        <el-tag style="margin-right:10px ;" v-for="(item) in tags" :key="item.key" @click="scorll(item.name)">{{ item.name }}</el-tag>
      </div>
    </div>
    <div class="yes-sir">
      <contrastCom ref='contrastCom' :contrast="showContrast" :column="column" />
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
  }, {
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
  }
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
      carOptions: [{
        label: '奔驰A',
        value: '1'
      }, {
        label: '奔驰B',
        value: '2'
      }, {
        label: '奔驰C',
        value: '3'
      }],
      tableHead: [
        { name: "车型", id: 0, key: 'name' },
        { name: "厂商指导价格", id: 2, key: 'theSameCreatePer' },
        { name: "经销商参考价", id: 3, key: 'issue' },
        { name: "口碑综合评分", id: 4, key: 'rate' },
        { name: "基本参数", id: 5, key: 'jiben' },
        { name: "厂商", id: 6, key: 'ipTheSame' },
        { name: "级别", id: 7, key: 'macTheSame' },
        { name: "能源类型", id: 5, key: 'existMatter' },
        { name: "环保标准", id: 6, key: 'personRep' },
        { name: "上市时间", id: 7, key: 'elsePer' },
        { name: "最大功率", id: 9, key: 'err' },
        { name: "最大扭矩", id: 10, key: 'quote' },
        { name: "车身", id: 1, key: 'cheshen' },
        { name: "厂商", id: 6, key: 'ipTheSame' },
        { name: "级别", id: 7, key: 'macTheSame' },
        { name: "能源类型", id: 5, key: 'existMatter' },
        { name: "环保标准", id: 6, key: 'personRep' },
        { name: "上市时间", id: 7, key: 'elsePer' },
        { name: "最大功率", id: 9, key: 'err' },
        { name: "最大扭矩", id: 10, key: 'quote' },
      ],
      tableBody: [
        {
          id: 1,
          name: '奔驰',
          issue: 5,
          rate: 3,
          theSameCreatePer: '是',
          theSameAmendPer: '是',
          ipTheSame: '是',
          macTheSame: '是',
          existMatter: '是',
          personRep: '是',
          elsePer: '是',
          err: '是',
          quote: '是',
          theRest: '无'
        },
        {
          id: 2,
          name: '宝马',
          issue: 10,
          rate: 4,
          theSameCreatePer: '否',
          theSameAmendPer: '否',
          ipTheSame: '否',
          macTheSame: '否',
          existMatter: '否',
          personRep: '否',
          elsePer: '否',
          err: '否',
          quote: '否',
          theRest: '有'
        },
        {
          id: 3,
          name: '奥迪',
          issue: 5,
          theSameCreatePer: '是',
          theSameAmendPer: '是',
          ipTheSame: '是',
          macTheSame: '是',
          existMatter: '是',
          personRep: '是',
          elsePer: '是',
          err: '是',
          quote: '是',
          theRest: '无'
        },
        {
          id: 4,
          name: '日产',
          issue: 10,
          theSameCreatePer: '否',
          theSameAmendPer: '否',
          ipTheSame: '否',
          macTheSame: '否',
          existMatter: '否',
          personRep: '否',
          elsePer: '否',
          err: '否',
          quote: '否',
          theRest: '有'
        },
        {
          id: 5,
          name: '奥迪2',
          issue: 5,
          theSameCreatePer: '是',
          theSameAmendPer: '是',
          ipTheSame: '是',
          macTheSame: '是',
          existMatter: '是',
          personRep: '是',
          elsePer: '是',
          err: '是',
          quote: '是',
          theRest: '无'
        },
        {
          id: 6,
          name: '日产2',
          issue: 10,
          theSameCreatePer: '否',
          theSameAmendPer: '否',
          ipTheSame: '否',
          macTheSame: '否',
          existMatter: '否',
          personRep: '否',
          elsePer: '否',
          err: '否',
          quote: '否',
          theRest: '有'
        },
        {
          id: 7,
          name: '日产3',
          issue: 10,
          theSameCreatePer: '否',
          theSameAmendPer: '否',
          ipTheSame: '否',
          macTheSame: '否',
          existMatter: '否',
          personRep: '否',
          elsePer: '否',
          err: '否',
          quote: '否',
          theRest: '有'
        },
      ],
      showCarList: [],
      rowList: [{
        key: 'row1',
        name: "车型",
        data: ['车型']
      },
      {
        key: 'row2',
        name: '厂商指导价',
        data: ['厂商指导价']
      }, {
        key: 'row3',
        name: "经销商参考价(元)",
        data: ['经销商参考价(元)']
      },
      {
        key: 'row4',
        name: '口碑综合评分',
        data: ['口碑综合评分']
      }],
      row2List: [{
        key: '',
        name: "车型",
        data: ['车型']
      },
      {
        key: 'row2',
        name: '厂商指导价',
        data: ['厂商指导价']
      }, {
        key: 'row3',
        name: "经销商参考价(元)",
        data: ['经销商参考价(元)']
      },
      {
        key: 'row4',
        name: '口碑综合评分',
        data: ['口碑综合评分']
      }],
      showContrast: [],
      tags: [{
        'name': '个性定义',
        key: "个性定义"
      }, {
        'name': '社交生活',
        key: "社交生活"
      }, {
        'name': '安全监测',
        key: "安全监测"
      }, {
        'name': '车辆服务',
        key: "车辆服务"
      }, {
        'name': '应急服务',
        key: "应急服务"
      }, {
        'name': '场景模式',
        key: "场景模式"
      }]
    }
  },
  methods: {
    scorll(id){
      this.$refs.contrastCom.scorll(id)
    },
    changeType (value) {
      const list = this.contrast.filter(item => value.includes(item.name))
      this.showContrast = list
      // this.transData(list)
    },
    transData (data) {
      this.rowList.forEach(x => {
        x.data = []
        x.data.push({
          key: x.key,
          name: x.name
        })
        data.forEach(item => {
          if (x.key === 'row1') {
            x.data.push({
              key: x.key,
              name: item.name
            })

          } else if (x.key === 'row2') {
            // x.data.push(item.issue)
            x.data.push({
              key: x.key,
              name: item.issue
            })
          } else if (x.key === 'row3') {

            x.data.push({
              key: x.key,
              name: item.theSameCreatePer
            })
          } else if (x.key === 'row4') {
            x.data.push({
              key: x.key,
              name: item.ipTheSame
            })
          }

        })
      })

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
    handleHeaderTitle (i) {
      if (i.key === 'issue') {
        return i.name + '(元)'
      }
      return i.name
    },
    changeType2 (value) {
      const list = this.tableBody.filter(item => value.includes(item.id))
      this.showCarList = list
    },
    extent (list) {
      var height = 50 * list.length
      return `height: ${height}px; line-height: ${height}px;`
    }
  },
  mounted () {
    this.transData([])
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

.menu-box {
  width: 140px;
  padding: 20px 20px 0 0;
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
  margin: 30px auto;
  border: solid 1px #eee;
}
</style>
