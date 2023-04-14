<template>
  <div class="content">
    <el-table ref="singleTable" :height="getHeight()" :data="targetArr" :show-header="true" :span-method="arraySpanMethod"
      border style="width: 100%" :cell-style="rowStyle" :header-cell-style="headerCellStyle">
      <el-table-column prop="00" align="center" width="180">
        <template slot="header" slot-scope="scope">
          <div>车型</div>
        </template>
        <template slot-scope="scope">
          <span :id="getId(scope.row[scope.column.property])">{{ scope.row[scope.column.property] }}</span>
        </template>
      </el-table-column>

      <el-table-column v-for="item in clumnArr" :key="item" :prop="String(item)" align="center" min-width="180">
        <template slot="header" slot-scope="scope">
          <div>{{ handleTitle(scope.column.property) }}</div>
        </template>
        <template slot-scope="scope">
          <div v-if="scope.row['00'] === '图片'">
            <img :src="scope.row[scope.column.property]" alt="">
          </div>
          <span v-else>{{ scope.row[scope.column.property] }}</span>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>
  
<script>
export default {
  name: 'Contrast',
  props: ['contrast', 'column'],
  data () {
    return {
      targetArr: [],
      clumnArr: [],
      listTwoRow: [0, 7, 10]
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
    getHeight(){
     const innerHeight= window.innerHeight
     return innerHeight-200
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
    scorll (id) {
      var table = this.$refs.singleTable;
      var height = table.$el.querySelector('.el-table__body-wrapper').clientHeight;
      var lastRowIndex = this.targetArr.length - 1;
      const index = this.column.findIndex(item => item.prop == id)
      const bodyWrapper = table.bodyWrapper
      const target = document.getElementById('1' + id)
      const top = this.getElementTop(target)
      bodyWrapper.scrollTo(0, top - 255);
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
        height: '100px',
        color: '#FFF',
        fontSize: "18px",
        backgroundColor: 'rgb(0 0 0)'
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
          background: '#efefef'
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
      return t.label
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
  
  