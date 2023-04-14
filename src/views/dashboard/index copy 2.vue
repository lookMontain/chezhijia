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
    <div class="content-box">
      <div class="menu-box">
        <div class="menu-item" @click="getScrollTo('jiben',0)">
          <div>
            基本参数
          </div>
          <div><i class="el-icon-arrow-right"></i></div>
        </div>
        <div class="menu-item" @click="getScrollTo('cheshen',1)" >
          <div>
            车身
          </div>
          <div><i class="el-icon-arrow-right"></i></div>
        </div>
      </div>
      <div class="box" id="box">
        <div class="tableHead">
          <el-row>
            <el-col :id="item.key" :class="{
              column: true,
              otherCol: item.key !== 'name',
              nameCol: item.key === 'name',
              secondLevelClass: item.key === 'jiben' || item.key === 'cheshen'
              
            }" v-for="(item, index) in tableHead" :key="index" :span="24">
              {{

                handleHeaderTitle(item)
              }}
            </el-col>
          </el-row>
        </div>
        <div class="tableBody">
          <template v-for="(i, j) in showCarList">
            <el-row :key="j" class="singleRow">
              <template v-for="(item, index) in tableHead">
                <el-col :span="24" :class="{
                  column: true,
                  otherCol: item.key !== 'name',
                  nameCol: item.key === 'name'
                }" :key="index">

                  <div style="width:180px; height: 100%;">
                    <template v-if="item.key === 'name'">
                      <div>
                        <div style="color: black">{{ i[item.key] }}</div>
                        <div class="name-bottom">
                          <div>厂商指导价：100w</div>
                          <el-link type="primary">询价</el-link>
                        </div>
                      </div>
                    </template>
                    <template v-else-if="item.key === 'issue'">
                      <div style="color: #ff8300;">
                        {{ i[item.key] }}
                        <el-link style="position: absolute; right:10px" type="primary">询价</el-link>
                      </div>
                    </template>
                    <template v-else-if="item.key === 'rate'">
                      <div style="width:100%; height: 100%; display: flex;align-items: center;">
                        <el-rate v-model="i[item.key]" disabled show-score text-color="#ff9900">
                        </el-rate>
                      </div>
                    </template>
                    <template v-else-if="item.key === 'elsePer' || item.key === 'err'">
                      <div style="width:100%; height: 100%;background: #f3f6fd;">
                        {{ i[item.key] }}
                      </div>
                    </template>
                    <template v-else-if="item.key === 'jiben'">
                      <div style="background-color: #f8f8f8;height: 100%;" id="jiben">

                      </div>
                    </template>
                    <template v-else>
                      {{ i[item.key] }}
                    </template>


                  </div>
                </el-col>
              </template>
            </el-row>
          </template>
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
      showCarList: []
    }
  },
  methods: {
    getScrollTo(id,i) {
      var element = document.getElementById('box');
      let offsetTop= document.querySelector(`#${id}`).offsetTop;  
      element.scrollTop = offsetTop-(i*40);
    },
    scrollIntoView(id){
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
    changeType (value) {
      const list = this.tableBody.filter(item => value.includes(item.id))
      this.showCarList = list
    },
    extent (list) {
      var height = 50 * list.length
      return `height: ${height}px; line-height: ${height}px;`
    }
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
.content-box{
  display: flex;
  overflow-y: scroll;
    padding: 10px;
    /* height: calc(100vh - 130px); */
}
</style>
