<template>
  <div class="chartBox">
    <div ref="dom" class="charts" />
  </div>
</template>

<script>
import echarts from 'echarts'
export default {
  name: 'PieChart',
  props: {
    name: {
      type: String,
      default: ''
    },
    unit: {
      type: String,
      default: ''
    },
    length: {
      type: Number,
      default: 0
    },
    legendData: {
      type: Array,
      default: () => {
        return []
      }
    },
    seriesData: {
      type: Array,
      default: () => {
        return []
      }
    }
  },
  data() {
    return {
      dom: null,
      isChange: true,
      timer: null
    }
  },
  destroyed() {
    clearInterval(this.timer)
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
    this.timer = setInterval(() => {
      that.setOption()
    }, 5000)
  },
  methods: {
    setOption() {
      const that = this
      const option = {
        title: {
          text: this.name,
          textStyle: {
            color: '#fff',
            fontSize: 14,
            fontWeight: 500
          },
          left: 'center',
          bottom: '48%'
        },
        tooltip: {
          trigger: 'item',
          formatter: '{a} <br/>{b}: {c} ({d}%)'
        },
        legend: {
          show: true,
          orient: 'horizontal',
          data: this.legendData,
          y: 'bottom',
          icon: 'circle',
          textStyle: {
            fontSize: 10,
            color: 'rgba(255,255,255,0.8)'
          }
        },
        series: [
          {
            name: this.name,
            type: 'pie',
            radius: ['40%', '50%'],
            center: ['50%', '45%'],
            avoidLabelOverlap: false,
            hoverAnimation: false,
            data: [
              {
                value: this.seriesData[0],
                name: this.legendData[0],
                label: {
                  formatter: `${this.seriesData[0]}${this.unit}`,
                  color: '#00E4FF'
                },
                labelLine: {
                  length2: this.length
                },
                itemStyle: {
                  normal: {
                    color: {
                      // 完成的圆环的颜色
                      colorStops: [
                        {
                          offset: 0,
                          color: '#14A0E8' // 0% 处的颜色
                        },
                        {
                          offset: 1,
                          color: '#00E4FF' // 100% 处的颜色
                        }
                      ]
                    }
                  }
                }
              },
              {
                value: this.seriesData[1],
                name: this.legendData[1],
                label: {
                  formatter: `${this.seriesData[1]}${this.unit}`,
                  color: '#D132FF'
                },
                labelLine: {
                  length: 5,
                  length2: 5
                },
                itemStyle: {
                  normal: {
                    color: {
                      colorStops: [
                        {
                          offset: 0,
                          color: '#BB42EF' // 0% 处的颜色
                        },
                        {
                          offset: 1,
                          color: '#D132FF' // 100% 处的颜色
                        }
                      ]
                    }
                  }
                }
              }
            ]
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
    .chartBox {
      width: 100%;
      height: 0;
      position: relative;
      padding-bottom: 55%;
      background: url("~@/assets/images/pie_base.png");
      background-repeat: no-repeat;
      background-size: 50%;
      background-position: center 76%;
      .charts {
        position: absolute;
        width: 100%;
        height: 100%;
      }
    }
  }
}
</style>
