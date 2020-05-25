<template>
  <div class="chartBox">
    <div ref="dom" class="charts" />
  </div>
</template>

<script>
import echarts from 'echarts'
export default {
  name: 'PieChart',
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
        title: {
          text: '人员',
          textStyle: {
            color: '#fff',
            fontSize: 16
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
          data: ['在岗人员', '离岗人员'],
          y: 'bottom',
          icon: 'circle',
          textStyle: {
            fontSize: 10,
            color: 'rgba(255,255,255,0.8)'
          }
        },
        series: [
          {
            name: '人员',
            type: 'pie',
            radius: ['40%', '50%'],
            center: ['50%', '45%'],
            avoidLabelOverlap: false,
            hoverAnimation: false,

            data: [
              {
                value: 335,
                name: '在岗人员',
                label: {
                  color: '#00E4FF'
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
                value: 31,
                name: '离岗人员',
                label: {
                  color: '#D132FF'
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
      padding-bottom: 50%;
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
