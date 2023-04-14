<template>
  <div style="padding: 20px;">
    <div>
      <el-form size="mini" :inline="true" :model="formInline" class="demo-form-inline">
        <el-form-item label="选择车型">
          <el-select v-model="formInline.carType" placeholder="车型" multiple @change="changeType" collapse-tags>
            <el-option v-for="(item) in tableBody" :key="item.id" :label="item.name" :value="item.id"></el-option>
          </el-select>
        </el-form-item>
        <!-- <el-form-item>
          <el-button type="primary" @click="onSubmit">查询</el-button>
        </el-form-item> -->
      </el-form>
    </div>
    <div>
      <div class="container-box">
        <div>
          <div v-for="(item) in rowList" class="row-box"
          :class="{
            row1Style:item.key=='row1'
          }"
  >
            <div v-for="(x,index) in item.data" class="row-item" :class="{
              row1itemStyle:item.key=='row1'&&index=='0'

            }" >
              <template v-if="x.key=='row1'&&index!==0">
                <div  class="row1-item">
                <div class="row1-title1"> {{ x.name}}</div> 
                <div  class="row1-title2"> 厂商指导价： 100w </div>
                </div>
              </template>

              <template v-else>
                {{ x.name}}
              </template>
       
            </div>
          </div>
        </div>

        <div class="container-detail">
          <div class="row1-1">
            基本参数
          </div>
          <div v-for="(item) in rowList" class="row-box">
            <div v-for="(x) in item.data" class="row-item">
              {{ x.name }}
            </div>
          </div>
          <div class="row1-1">
            车身
          </div>
          <div v-for="(item) in rowList" class="row-box">
            <div v-for="(x) in item.data" class="row-item">
              {{ x.name  }}
            </div>
          </div>
          <div class="row1-1">
            电动机
          </div>
          <div v-for="(item) in rowList" class="row-box">
            <div v-for="(x) in item.data" class="row-item">
              {{ x.name  }}
            </div>
          </div>
        </div>

      </div>

    </div>

  </div>
</template>

<script>
export default {
  name: 'dashboard',
  data () {
    return {
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
    }
  },
  methods: {
    changeType (value) {
      const list = this.tableBody.filter(item => value.includes(item.id))
      this.showCarList = list
      this.transData(list)
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
.row1Style{
  height: 130px;
  background: #f8f8f8;
}
.row1-item{
  height: 100%;
  display: flex;
  justify-content: center;
  flex-direction: column;
}
.row1-item >div{
  text-align: center;
}
.row1-title1{
  font-size: 20px;
  font-weight: 800;
}
.row1-title2{
  color: #ff9600;
    margin: 5px 0;
}
.row1itemStyle{
  line-height: 130px;
  text-align: center;
}
</style>
