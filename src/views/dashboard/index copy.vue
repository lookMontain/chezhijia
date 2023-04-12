<template>
  <div>
    <el-table border style="margin-top: 50px;" :data="transData" :show-header="false">
      <el-table-column v-for="(item, index) in transTitle" :label="item" :key="index" align="center">
        <template slot-scope="scope">
          {{ scope.row[index] }}
        </template>
      </el-table-column>
    </el-table>

  </div>
</template>

<script>

export default {
  name: "kehu",
  components: {
  },
  data () {
    return {
      originData: [{
        '车型': '奔驰1',
        '经销商参考价': '100w',
        '厂商指导价格': '10w',
        '厂商':'绍兴',
        '级别':1,
        '能源类型':2,
        '环保标准':3,
        '上市时间':4,
        '最大功率':5,
        '最大扭矩':6
      },
      {
        '车型': '奔驰2',
        '经销商参考价': '100w',
        '厂商指导价格': '10w',
        '厂商':'绍兴',
        '级别':1,
        '能源类型':2,
        '环保标准':3,
        '上市时间':4,
        '最大功率':5,
        '最大扭矩':6
      },
      {
        '车型': '奔驰3',
        '经销商参考价': '100w',
        '厂商指导价格': '10w',
        '厂商':'绍兴',
        '级别':1,
        '能源类型':2,
        '环保标准':3,
        '上市时间':4,
        '最大功率':5,
        '最大扭矩':6
      }
      ],
      originTitle: ['车型','经销商参考价', '厂商指导价格', '厂商','级别','能源类型','环保标准','上市时间','最大功率','最大扭矩'], // originTitle 该标题为 正常显示的标题, 数组中的顺序就是上面数据源对象中的字段标题对应的顺序
      transTitle: ['', '学生1', '学生2', '学生3'], // transTitle 该标题为转化后的标题, 注意多一列,  因为原来的标题变成了竖着显示了, 所以多一列标题, 第一个为空即可
      transData: []
    };
  },
  mounted () {
    // 数组按矩阵思路, 变成转置矩阵
    let matrixData = this.originData.map((row) => {
      let arr = []
      for (let key in row) {
        arr.push(row[key])
      }
      return arr
    })
    console.log(matrixData)
    // 加入标题拼接最终的数据
    this.transData = matrixData[0].map((col, i) => {
      return [this.originTitle[i], ...matrixData.map((row) => {
        return row[i]
      })]
    })
    console.log(this.transData)
  },
  methods: {

    handleCellclass ({ column, columnIndex }) {
      if (columnIndex !== 0 && column.label.indexOf("识别结果") !== -1) {
        return "tableColumnClass"
      } else {
        return ''
      }
    }
  }
};
</script>
<style scoped>
.row {
  margin: 5px -5px;

}
</style>

