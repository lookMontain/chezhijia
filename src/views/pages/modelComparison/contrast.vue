<template>
  <div class="content">
    <el-table ref="singleTable" :height="getHeight()" :data="targetArr" :show-header="true" :span-method="arraySpanMethod"
      border style="width: 100%" :cell-style="rowStyle" :header-cell-style="headerCellStyle">
      <el-table-column prop="00" align="center" width="180">
        <template slot="header" slot-scope="scope">
          <div>车型</div>
        </template>
        <template slot-scope="scope">
          <div :id="getId(scope.row[scope.column.property])">
            <template v-if="handleGroupRow(scope.$index)">
              <el-tag effect="plain" type="success" style="font-size: 16px;font-weight: 600;">
                {{ scope.row[scope.column.property] }}
              </el-tag>
            </template>
            <template v-else>
              <el-link style="color:#2f6ad6" type="primary" @click="showDetail(scope.row, scope.column.property)"> {{
                scope.row[scope.column.property] }}</el-link>
            </template>

          </div>
        </template>
      </el-table-column>
      <el-table-column v-for="(item,index) in clumnArr" :key="index" :prop="String(item)" align="center" width="180">
        <template slot="header" slot-scope="scope">
          <div>{{ handleTitle(scope.column.property) }}</div>
        </template>
        <template slot-scope="scope">
          <span @click="showSingleDetail(scope.row, scope.column.property, scope.column)">{{ handleValue(scope.row,
            scope.column.property) }}</span>
        </template>
      </el-table-column>
    </el-table>
    <el-dialog :title="dialogTitle" :visible.sync="dialogVisible" width="80%" :before-close="handleClose">


      <el-table ref="singleTable2" :height="400" :data="targetArr2" :show-header="true" border
        :style="{ width: clumnArr2.length * 180 + 'px' }">
        <el-table-column prop="00" align="center" width="180">
          <template slot="header" slot-scope="scope">
            <div>车型</div>
          </template>
          <template slot-scope="scope">
            <div>
              <span :style="{
                color: scope.row[scope.column.property] === '整体评分' ? 'red' : '#2f6ad6',
                'font-weight': 500
              }"> {{scope.row[scope.column.property] }}</span>
            </div>
          </template>

        </el-table-column>
        <el-table-column v-for="item in clumnArr2" :key="item" :prop="String(item)" align="center" width="180">
          <template slot="header" slot-scope="scope">
            <div>{{ handleTitle(scope.column.property) }}</div>
          </template>
          <template slot-scope="scope">
            <span>{{ handleValueDialog(scope.row[scope.column.property]) }}</span>
          </template>
        </el-table-column>
      </el-table>

      <span slot="footer" class="dialog-footer">
        <el-button type="primary" size="mini" @click="dialogVisible = false">关闭窗口</el-button>
      </span>
    </el-dialog>
    <el-dialog :title="singleDetailTitle" :visible.sync="singleDetail" width="900">
      <el-descriptions title="" :column="3" border>
        <el-descriptions-item label="功能丰富">{{ singleDetailData['功能丰富性'] }}</el-descriptions-item>
        <el-descriptions-item label="逻辑合理">{{ singleDetailData['功能逻辑'] }}</el-descriptions-item>
        <el-descriptions-item label="交互便捷">
          {{ singleDetailData['使用便捷性'] }}
        </el-descriptions-item>
        <el-descriptions-item label="视觉美观">
          {{ singleDetailData['视觉效果'] }}
        </el-descriptions-item>
        <el-descriptions-item label="功能可靠"> {{ singleDetailData['功能稳定性'] }}</el-descriptions-item>
        <el-descriptions-item label="使用安全">{{ singleDetailData['安全性'] }}</el-descriptions-item>
        <el-descriptions-item label="整体评分"><el-tag size="small">{{ singleDetailData['整体评分']
        }}</el-tag></el-descriptions-item>
      </el-descriptions>
      <span slot="footer" class="dialog-footer">
        <el-button type="primary" size='mini' @click="singleDetail = false">关闭窗口</el-button>
      </span>
    </el-dialog>
  </div>
</template>
  
<script>
import { cloneDeep } from 'lodash'
export default {
  name: 'Contrast',
  props: ['contrast', 'column'],
  data () {
    return {
      tableData: [{
          id: '12987122',
          name: '王小虎',
          amount1: '234',
          amount2: '3.2',
          amount3: 10
        }, {
          id: '12987123',
          name: '王小虎',
          amount1: '165',
          amount2: '4.43',
          amount3: 12
        }, {
          id: '12987124',
          name: '王小虎',
          amount1: '324',
          amount2: '1.9',
          amount3: 9
        }, {
          id: '12987125',
          name: '王小虎',
          amount1: '621',
          amount2: '2.2',
          amount3: 17
        }, {
          id: '12987126',
          name: '王小虎',
          amount1: '539',
          amount2: '4.1',
          amount3: 15
        }],
      targetArr: [],
      clumnArr: [],
      dialogVisible: false,
      column2: [{
        label: '整体评分',
        prop: '整体评分'
      }, {
        label: '功能丰富',
        prop: '功能丰富性',
      },
      {
        label: '逻辑合理',
        prop: '功能逻辑'
      },
      {
        label: '交互便捷',
        prop: '使用便捷性',
      },
      {
        label: '视觉美观',
        prop: '视觉效果'
      },
      {
        label: '功能可靠',
        prop: '功能稳定性'
      }, {
        label: '使用安全',
        prop: '安全性'
      }],
      contrast2: [
        {
          "name": "星越L",
          label: '星越L',
          '功能丰富': '2',
          逻辑合理: '3',
        },

        {
          "name": "岚图Free",
          label: '岚图Free',
          '功能丰富': '2',
          逻辑合理: '3',
        }],
      clumnArr2: [],
      targetArr2: [],
      dialogTitle: '详情',
      singleDetail: false,
      singleDetailData: {
        整体评分: '',
        功能丰富性: "",
        功能逻辑: '',
        使用便捷性: '',
        视觉效果: '',
        功能稳定性: '',
        安全性: ''
      },
      singleDetailTitle: ''
    }
  },
  watch: {
    contrast: {
      handler () {
        this.getChangeData()

      },
      immediate: true
    }
  },
  created () {
    this.getChangeData()
  },
  methods: {
    showSingleDetail (row, prop, c) {
      const title = this.handleTitle(prop)
      const obj = row[prop]
      this.singleDetailTitle = `满意度构成维度: ` + row['00'] + ' - ' + title
      this.singleDetailData = {}
      Object.keys(obj).forEach(key => {
        if (obj[key]) {
          this.singleDetailData[key] = Number(obj[key]).toFixed(2)
        } else {
          this.singleDetailData[key] = '-'
        }

      })

      this.singleDetail = true
    },
    handleValueDialog (value) {
      if (value) {
        return Number(value).toFixed(2)
      } else {
        return '-'
      }
    },
    handleValue (row, property) {
      const target = this.column.find(item => item.prop === row['00'] && item.isGroup)
      if (target) return
      const value = row[property] && row[property]['整体评分']
      if (value) {
        return Number(value).toFixed(2)
      } else {
        return '-'
      }

    },
    randomNumBoth (Min = 10, Max = 500) {
      var Range = Max - Min;
      var Rand = Math.random();
      var num = Min + Math.round(Rand * Range); //四舍五入
      return num;
    },
    handleClose () {
      this.dialogVisible = false
    },
    showDetail (row, perty) {
      console.log(row, perty)
      this.dialogTitle = `满意度构成维度: ` + row[perty]
      const list = cloneDeep(this.contrast).map(item => {
        const _dialogTitleValue = item[row[perty]] || {}
        return {
          'name': item.name,
          ..._dialogTitleValue

        }
      })
      this.contrast2 = list
      this.getChangeData2()
      this.dialogVisible = true

    },
    getHeight () {
      const innerHeight = window.innerHeight
      return innerHeight - 230
    },
    getElementTop (element) {
      var actualTop = element.offsetTop;
      var current = element.offsetParent;
      while (current !== null) {
        actualTop += current.offsetTop;
        current = current.offsetParent;
      }
      return actualTop;
    },
    scorll (id, indext) {
      var table = this.$refs.singleTable;
      const bodyWrapper = table.bodyWrapper
      const target = document.getElementById('1' + id)
      const top = this.getElementTop(target)
      const mScrollTop = document.getElementById('menuBox').scrollTop
      const x = indext === 0 ? 80 : 40
      bodyWrapper.scrollTo(0, top - 192 - (indext * 48) + mScrollTop - x);
      // var scrollPosition = target.offsetTop - height + target.clientHeight;
      // table.scrollToRow(index);
      // table.scrollToRow(lastRowIndex, scrollPosition);
      // const table = this.$refs.singleTable
      // const b = table.bodyWrapper
      // const target = document.getElementById('1' + id)
      // b.scrollTop = target.offsetTop
    },
    getId (id) {
      return '1' + id
    },
    headerCellStyle () {
      return {
        height: '40px',
        color: '#FFF',
        fontSize: "16px",
        backgroundColor: '#000'
      }
    },
    handleGroupRow (index) {
      const list = []
      this.column.forEach((item, index) => {
        if (item.isGroup) {
          list.push(index)
        }
      })
      if (list.includes(index)) return true
    },
    rowStyle (row) {
      if (this.handleGroupRow(row.rowIndex)) {
        return {
          'text-align': 'left',
          background: '#f8fafb',
          padding: '5px 0',
          'border-right': 'none'
        }
      } else {
        return {
          padding: '5px 0'
        }
      }
    },
    arraySpanMethod ({ row, column, rowIndex, columnIndex }) {
      return undefined
      if (this.handleGroupRow(rowIndex)) {
        return [1, 9];
      }else{
        return undefined
      }
    },

    handleTitle (p) {
      const t = this.contrast[p]
      return t.name
    },
    getChangeData () {
      const clumnArr = [...new Array(this.contrast.length).keys()] // 改变数据，根据数据的长度生成数组，作为table的column的prop
      const targetArr = [] // 数据数组
      /**
       * 下面则是将原数组转为合适数据
      */
      const tableData = []
      let objKey = []

      // 第一步将原数组中对象的key变为左侧需要展示的文字
      this.contrast.forEach(ele => {
        const obj = {}
        this.column.forEach(item => {
          obj[item.label] = ele[item.prop]
        })
        Object.keys(obj).forEach((item) => {
          objKey.push(item)
        })
        tableData.push(obj)
      })

      // 将所有的key值放到数组中
      objKey = [...new Set(objKey)]

      // 根据左侧值遍历数组
      for (let i = 0; i < objKey.length; i++) {
        const obj = {}
        for (let m = 0; m < tableData.length; m++) {
          obj[m] = tableData[m][objKey[i]]
        }
        targetArr.push(obj)
      }

      // 新增一个00作为左侧第一列的prop
      targetArr.forEach((ele, index) => {
        ele['00'] = objKey[index]
      })

      this.targetArr = targetArr
      this.clumnArr = clumnArr
      this.$nextTick(() => {
        this.$refs.singleTable.doLayout()
      })
    },
    getChangeData2 () {
      const clumnArr = [...new Array(this.contrast2.length).keys()] // 改变数据，根据数据的长度生成数组，作为table的column的prop
      const targetArr = [] // 数据数组
      /**
       * 下面则是将原数组转为合适数据
      */
      const tableData = []
      let objKey = []

      // 第一步将原数组中对象的key变为左侧需要展示的文字
      this.contrast2.forEach(ele => {
        const obj = {}
        this.column2.forEach(item => {
          obj[item.label] = ele[item.prop]
        })
        Object.keys(obj).forEach((item) => {
          objKey.push(item)
        })
        tableData.push(obj)
      })

      // 将所有的key值放到数组中
      objKey = [...new Set(objKey)]

      // 根据左侧值遍历数组
      for (let i = 0; i < objKey.length; i++) {
        const obj = {}
        for (let m = 0; m < tableData.length; m++) {
          obj[m] = tableData[m][objKey[i]]
        }
        targetArr.push(obj)
      }

      // 新增一个00作为左侧第一列的prop
      targetArr.forEach((ele, index) => {
        ele['00'] = objKey[index]
      })

      this.targetArr2 = targetArr
      this.clumnArr2 = clumnArr
    }
  }

}
</script>
  
<style scoped>
.content {
  width: 100%;
  position: relative;
}
</style>
  