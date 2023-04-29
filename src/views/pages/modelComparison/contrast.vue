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
              <el-tag type="success" style="font-size: 16px;font-weight: 600;">
                {{ scope.row[scope.column.property] }}
              </el-tag>
            </template>
            <template v-else>
              <el-link type="primary" @click="showDetail(scope.row, scope.column.property)"> {{
                scope.row[scope.column.property] }}</el-link>
            </template>

          </div>
        </template>
      </el-table-column>
      <el-table-column v-for="item in clumnArr" :key="item" :prop="String(item)" align="center" min-width="180">
        <template slot="header" slot-scope="scope">
          <div>{{ handleTitle(scope.column.property) }}</div>
        </template>
        <template slot-scope="scope">
          <span>{{ handleValue(scope.row, scope.column.property) }}</span>
        </template>
      </el-table-column>
    </el-table>
    <el-dialog :title="dialogTitle" :visible.sync="dialogVisible" width="90%" :before-close="handleClose">
      <el-table ref="singleTable2" :height="400" :data="targetArr2" :show-header="true" border style="width: 100%">
        <el-table-column prop="00" align="center" width="180">
          <template slot="header" slot-scope="scope">
            <div>车型</div>
          </template>
        </el-table-column>
        <el-table-column v-for="item in clumnArr2" :key="item" :prop="String(item)" align="center" min-width="180">
          <template slot="header" slot-scope="scope">
            <div>{{ handleTitle(scope.column.property) }}</div>
          </template>
          <template slot-scope="scope">
            <span>{{ handleValueDialog(scope.row[scope.column.property])  }}</span>
          </template>
        </el-table-column>
      </el-table>
      <span slot="footer" class="dialog-footer">
        <el-button type="primary" size="mini" @click="dialogVisible = false">关闭窗口</el-button>
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
      targetArr: [],
      clumnArr: [],
      dialogVisible: false,
      column2: [{
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
      dialogTitle: '详情'
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
    handleValueDialog(value){
      if (value) {
        return Number(value).toFixed(2)
      }
    },
    handleValue (row, property) {
      const value = row[property] && row[property]['整体评分']
      if (value) {
        return Number(value).toFixed(2)
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
      this.dialogTitle = row[perty]
      debugger
      const list = cloneDeep(this.contrast).map(item => {
        const _dialogTitleValue = item[this.dialogTitle] || {}
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
      return innerHeight - 150
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
      bodyWrapper.scrollTo(0, top - 192 - (indext * 43) + mScrollTop);
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
        height: '60px',
        color: '#FFF',
        fontSize: "18px",
        backgroundColor: 'rgb(140 140 140)'
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
          background: '#f8f8f8',
          padding: '5px 0'
        }
      } else {
        return {
          padding: '5px 0'
        }
      }
    },
    arraySpanMethod ({ row, column, rowIndex, columnIndex }) {
      if (this.handleGroupRow(rowIndex)) {
        return [1, 9];
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
  
  