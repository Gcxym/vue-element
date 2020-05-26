<template>
  <div class="barChart">
    <div class="bar-info">
      <div class="bar-item">
        <div>
          <p>2019年</p>
          <p>总产值：</p>
        </div>
        <div>
          889.0
          <span>万元</span>
        </div>
      </div>
      <div class="bar-item">
        <div>
          <p>2020年</p>
          <p>总产值：</p>
        </div>
        <div>
          889.0
          <span>万元</span>
        </div>
      </div>
    </div>
    <div class="chartBox">
      <div ref="dom" class="charts" />
    </div>
  </div>
</template>

<script>
import echarts from 'echarts'
export default {
  name: 'BarChart',
  data() {
    return {
      dom: null,
      isChange: true
    }
  },
  mounted() {
    const that = this
    that.dom = echarts.init(that.$refs.dom)
    that.$nextTick(() => {
      that.setOption()
      that.dom.resize()
      window.addEventListener('resize', function() {
        that.dom.resize()
      })
    })
  },
  methods: {
    setOption() {
      const that = this
      const option = {
        color: ['#35D0E9', '#904AFD'],
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'shadow'
          }
        },
        grid: {
          left: 10,
          right: 10,
          bottom: 20,
          top: 30,
          containLabel: true
        },
        legend: {
          data: ['2019年', '2020年'],
          icon: 'circle',
          right: 0,
          textStyle: {
            color: 'rgba(255,255,255,0.8)'
          }
        },
        xAxis: [
          {
            type: 'category',
            axisTick: { show: false },
            data: ['一季度', '二季度', '三季度', '四季度'],
            axisLine: {
              lineStyle: {
                color: '#B9C8DB'
              }
            }
          }
        ],
        yAxis: [
          {
            type: 'value',
            name: '（万元）',
            axisTick: { show: false },
            axisLine: {
              lineStyle: {
                color: '#B9C8DB'
              }
            },
            splitLine: {
              show: true,
              lineStyle: {
                color: 'rgba(242,242,242,0.2)'
              }
            }
          }
        ],
        series: [
          {
            z: 1,
            name: '2019年',
            type: 'bar',
            barGap: 0,
            barWidth: '30%',
            data: [200, 350, 250, 420],
            itemStyle: {
              normal: {
                // 设置渐变色
                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                  { offset: 0, color: '#00A2DB' },
                  { offset: 1, color: '#35D0E9' }
                ])
              }
            }
          },
          {
            z: 2,
            name: '2019年',
            type: 'pictorialBar',
            symbolPosition: 'end',
            data: [200, 350, 250, 420],
            symbol: 'diamond',
            symbolOffset: ['-50%', '-50%'],
            symbolSize: ['38%', '15%'],
            itemStyle: {
              normal: {
                // 设置渐变色
                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                  { offset: 0, color: '#00A2DB' },
                  { offset: 1, color: '#35D0E9' }
                ])
              }
            }
          },
          {
            name: '2020年',
            type: 'bar',
            barWidth: '30%',
            data: [120, 270, 170, 350],
            itemStyle: {
              normal: {
                // 设置渐变色
                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                  { offset: 0, color: '#4E15D2' },
                  { offset: 1, color: '#904AFD' }
                ])
              }
            }
          },
          {
            z: 3,
            name: '2020年',
            type: 'pictorialBar',
            symbolPosition: 'end',
            data: [120, 270, 170, 350],
            symbol: 'diamond',
            symbolOffset: ['50%', '-50%'],
            symbolSize: ['38%', '15%'],
            itemStyle: {
              normal: {
                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                  { offset: 0, color: '#4E15D2' },
                  { offset: 1, color: '#904AFD' }
                ])
              }
            }
          }
        ]
      }
      that.dom.clear()
      that.dom.setOption(option)
    }
  }
}
</script>

<style lang="scss" scoped>
.large-container {
  .large-chart {
    .barChart {
      width: 100%;
      height: 85%;
      .bar-info {
        display: flex;
        justify-content: space-between;
        color: rgba(255, 255, 255, 0.8);
        padding: 0 20px;
        margin: 15px 0;
        .bar-item {
          display: flex;
          align-items: center;
          p {
            margin: 0;
            font-size: 12px;
          }
          & > div:nth-child(2) {
            color: #00bbff;
            font-size: 20px;
            font-weight: 600;
            span {
              font-size: 12px;
            }
          }
        }
      }
    }
    .chartBox {
      width: 100%;
      height: 0;
      position: relative;
      padding-bottom: 50%;
      .charts {
        position: absolute;
        width: 100%;
        height: 100%;
      }
    }
  }
}
</style>
