<template>
  <div class="chartBox">
    <div ref="dom" class="charts" />
  </div>
</template>

<script>
import echarts from 'echarts'
import 'echarts/map/js/world.js'
import 'echarts-gl'

export default {
  name: 'GlobeChart',
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
        globe: {
          show: true,
          baseTexture: require('@/assets/images/earthCopy.png'),
          displacementScale: 0.4,
          globeRadius: 70,
          shading: 'lambert',
          light: {
            ambient: {
              intensity: 1.0
            },
            main: {
              intensity: 0
            }
          },
          viewControl: {
            targetCoord: [110.46, 10.92]
          },
          layers: [
            {
              type: 'overlay',
              texture: require('@/assets/images/dottedLine.png'),
              shading: 'lambert',
              distance: 10
            },
            {
              type: 'overlay',
              texture: require('@/assets/images/solidLine.png'),
              shading: 'lambert',
              distance: 5
            }
          ]
        },
        series: [
          {
            type: 'lines3D',
            effect: {
              show: true,
              period: 3,
              trailLength: 0.1
            },
            lineStyle: {
              color: '#9ae5fc',
              width: 1,
              opacity: 1
            },
            tooltip: {
              show: true,
              trigger: 'item',
              formatter() {
                return 'jhfjdsagfjsdgfisdgfiusagfuiasgf'
              }
            },
            data: [
              {
                coords: [
                  [107.7539, 30.1904, 0],
                  [135.193845, -25.304039, 0]
                ]
              },
              {
                coords: [
                  [107.7539, 30.1904, 0],
                  [-100.696295, 33.679979, 0]
                ]
              },
              {
                coords: [
                  [107.7539, 30.1904, 0],
                  [113.5107, 23.2196, 0]
                ]
              },
              {
                coords: [
                  [107.7539, 30.1904, 0],
                  [7.445147, 46.956241]
                ]
              }
            ]
          },
          {
            type: 'scatter3D',
            name: 'location',
            coordinateSystem: 'globe',
            blendMode: 'lighter',
            symbolSize: 10,
            itemStyle: {
              color: '#B03A5B',
              opacity: 1,
              borderColor: '#B03A5B'
            },

            emphasis: {
              itemStyle: {
                color: '#B03A5B'
              }
            },
            data: [
              {
                name: '重庆',
                value: [107.7539, 30.1904, 0],
                label: {
                  show: true,
                  formatter: '南京建设公司城建智慧工地'
                }
              },
              {
                name: '广州',
                value: [113.5107, 23.2196, 0],
                label: {
                  show: true,
                  formatter: '广州建设公司城建智慧工地'
                }
              },
              {
                name: '美国',
                value: [-100.696295, 33.679979, 0],
                label: {
                  show: true,
                  formatter: '美国建设公司城建智慧工地'
                }
              },
              {
                name: '澳大利亚',
                value: [135.193845, -25.304039, 0],
                label: {
                  show: true,
                  formatter: '澳大利亚公司'
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
  .chartBox {
    width: 100%;
    height: 0;
    position: relative;
    padding-bottom: 80%;
    background: url("~@/assets/images/bg_light.png");
    background-repeat: no-repeat;
    background-size: 200%;
    background-position: center bottom;
    .charts {
      position: absolute;
      width: 100%;
      height: 100%;
    }
  }
}
</style>
