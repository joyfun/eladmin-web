<template>
  <div class="dashboard-container">
    <div class="dashboard-editor-container">

      <el-row style="background:#fff;padding:16px 16px 0;margin-bottom:32px;">
        <el-col :xs="8" :sm="12" :lg="8" class="card-panel-col">
          <line-chart :chart-data="lineChartData" />

        </el-col>
        <el-col :xs="8" :sm="12" :lg="8" class="card-panel-col">
          <scatter-chart :chart-data="lineChartData" />

        </el-col>
        <el-col :xs="8" :sm="12" :lg="8" class="card-panel-col">
          <line-chart :chart-data="lineChartData" />

        </el-col>

      </el-row>
      <el-row style="background:#fff;padding:16px 16px 0;margin-bottom:32px;">
        <line-chart :chart-data="lineChartData" />

        <scatter-chart :chart-data="lineChartData" />

      </el-row>
      <el-row style="background:#fff;padding:16px 16px 0;margin-bottom:32px;">
        <line-chart :chart-data="lineChartData" />

        <scatter-chart :chart-data="lineChartData" />

      </el-row>

    </div>
  </div>
</template>

<script>
// import GithubCorner from '@/components/GithubCorner'
import ScatterChart from './ScatterChart'
import LineChart from './LineChart'

// import RadarChart from '@/components/Echarts/RadarChart'
// import PieChart from '@/components/Echarts/PieChart'
// import BarChart from '@/components/Echarts/BarChart'

const lineChartData = {
  newVisitis: {
    expectedData: [100, 120, 161, 134, 105, 160, 165, 177, 124, 201, 169, 183],
    actualData: [120, 82, 91, 154, 162]
  },
  messages: {
    expectedData: [200, 192, 120, 144, 160, 130, 140],
    actualData: [180, 160, 151, 106, 145, 150, 130]
  },
  purchases: {
    expectedData: [80, 100, 121, 104, 105, 90, 100],
    actualData: [120, 90, 100, 138, 142, 130, 130]
  },
  shoppings: {
    expectedData: [130, 140, 141, 142, 145, 150, 160],
    actualData: [120, 82, 91, 154, 162, 140, 130]
  }
}

export default {
  name: 'Dashboard',
  components: {
    LineChart,
    ScatterChart
  },
  data() {
    return {
      lineChartData: lineChartData.newVisitis
    }
  },
  methods: {
    handleSetLineChartData(type) {
      this.lineChartData = lineChartData[type]
    }
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
  .dashboard-editor-container {
    padding: 32px;
    background-color: rgb(240, 242, 245);
    position: relative;

    .github-corner {
      position: absolute;
      top: 0;
      border: 0;
      right: 0;
    }

    .chart-wrapper {
      background: #fff;
      padding: 16px 16px 0;
      margin-bottom: 32px;
    }
  }

  @media (max-width:1024px) {
    .chart-wrapper {
      padding: 8px;
    }
  }
</style>
