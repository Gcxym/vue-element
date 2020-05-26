<template>
  <div class="chartBox">
    <div ref="dom" class="charts" />
  </div>
</template>

<script>
import echarts from 'echarts'
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
      const chart = echarts.init(document.createElement('canvas'), null, {
        width: 4096,
        height: 2048
      })
      chart.setOption({
        tooltip: {
          backgroundColor: 'red',
          alwaysShowContent: true
          // formatter(item) {
          //   return 'jhfjdsagfjsdgfisdgfiusagfuiasgf'
          // }
        },
        geo: {
          type: 'map',
          map: 'world',
          left: 0,
          top: 0,
          right: 0,
          bottom: 0,
          zoom: 0,
          boundingCoords: [
            [-180, 90],
            [180, -90]
          ],
          roam: false,
          itemStyle: {
            borderColor: '#000d2d',
            areaColor: '#2455ad',
            emphasis: {
              areaColor: '#357cf8'
            }
          },
          label: {
            fontSize: 24
          }
        },
        series: [
          {
            type: 'effectScatter',
            coordinateSystem: 'geo',
            zlevel: 3,
            rippleEffect: {
              brushType: 'stroke'
            },
            label: {
              show: true,
              position: 'left',
              fontSize: 18,
              formatter: '{b}'
            },
            itemStyle: {
              normal: {
                color: '#ff0000'
              }
            },
            data: [
              {
                name: '重庆',
                value: [107.7539, 30.1904],
                symbolSize: parseInt(Math.random() * 20 + 10),
                label: {
                  position: 'right'
                }
              }
            ]
          }
        ]
      })
      // baseTexture: chart;
      const option = {
        globe: {
          show: true,
          baseTexture: require('@/assets/images/earth.jpg'),
          // baseTexture: chart,
          displacementScale: 0.1,
          globeRadius: 70,
          shading: 'lambert',
          light: {
            ambient: {
              intensity: 1.0
            },
            main: {
              intensity: 1.0
            }
          }
        },
        series: [
          // {
          //   type: 'scatter3D',
          //   name: 'location',
          //   coordinateSystem: 'globe',
          //   blendMode: 'lighter',
          //   symbolSize: 10,
          //   itemStyle: {
          //     color: '#B03A5B',
          //     opacity: 1
          //   },
          //   label: {
          //     show: true,
          //     formatter: '南京建设公司城建智慧工地'
          //   },
          //   data: [
          //     {
          //       name: '重庆',
          //       value: [107.7539, 30.1904, 0]
          //     }
          //   ]
          // }
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
