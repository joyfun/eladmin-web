<template>
  <div :class="className" :style="{height:height,width:width}" />
</template>

<script>
import echarts from 'echarts'
require('echarts/theme/macarons') // echarts theme
import resize from './mixins/resize'

export default {
  mixins: [resize],
  props: {
    className: {
      type: String,
      default: 'chart'
    },
    width: {
      type: String,
      default: '100%'
    },
    height: {
      type: String,
      default: '350px'
    },
    autoResize: {
      type: Boolean,
      default: true
    },
    chartData: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      chart: null
    }
  },
  watch: {
    chartData: {
      deep: true,
      handler(val) {
        this.setOptions(val)
      }
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.initChart()
    })
  },
  beforeDestroy() {
    if (!this.chart) {
      return
    }
    this.chart.dispose()
    this.chart = null
  },
  methods: {
    initChart() {
      this.chart = echarts.init(this.$el, 'macarons')
      this.setOptions(this.chartData)
    },
    setOptions({ expectedData, actualData } = {}) {
      var markLineOpt = {
        animation: false,
        label: {
          formatter: 'y =  2.2* x + 3',
          align: 'right'
        },
        lineStyle: {
          type: 'solid'
        },
        // tooltip: {
        //   formatter: 'y =  * x + 3'
        // },
        data: [[{
          coord: [0, 1000],
          symbol: 'none'
        }, {
          coord: [100000, 100000],
          symbol: 'none'
        }]]
      }
      this.chart.setOption({
        title: {
          text: '制冷机房能效对比'
        },
        xAxis: {
        //  data: ['10000', '20000', '30000', '40000', '50000', '60000', '70000'],
          boundaryGap: false,
          axisTick: {
            show: false
          }
        },
        grid: {
          left: 10,
          right: 10,
          bottom: 20,
          top: 30,
          containLabel: true
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'cross'
          },
          padding: [5, 10]
        },
        yAxis: {
          axisTick: {
            show: false
          }
        },
        legend: {
          data: ['制冷量', '耗电量']
        },
        series: [{
          symbolSize: 20,
          name: ['制冷量', '耗电量'],
          data: [
            [1232.0, 83434.04],
            [12323.0, 63434.95],
            [24242.0, 73434.58],
            [56778.0, 83434.81],
            [32122.0, 85552.33],
            [41223.0, 92323.96],
            [51232.0, 72323.24],
            [80992.0, 42323.26],
            [63471.0, 123230.84],
            [10582.0, 42332.82],
            [44124.0, 53232.68]
          ],
          markLine: markLineOpt,
          type: 'scatter'
        },
        {
          symbolSize: 20,
          //  name: ['expected', 'actual'],
          data: [
            [2232.0, 73434.04],
            [32323.0, 53434.95],
            [44242.0, 63434.58],
            [66778.0, 73434.81],
            [52122.0, 65552.33],
            [71223.0, 82323.96],
            [41232.0, 62323.24],
            [90992.0, 52323.26],
            [53471.0, 113230.84],
            [9582.0, 32332.82],
            [64124.0, 63232.68]
          ],
          markLine: markLineOpt,
          type: 'scatter'
        }]
      })
    }
  }
}
</script>
