<template>
  <div class="large-container">
    <div class="large-name">
      <img :src="srcName" alt>
      <span class="large-time">{{ time }}</span>
      <span class="large-address">当前位置：{{ address }}</span>
    </div>
    <div class="large-content">
      <div class="large-left">
        <div class="large-left-num">
          <div v-for="(item,index) in underNum" :key="index">{{ item }}</div>
          <p>
            <img :src="itemImg" alt>
            在建项目
          </p>
        </div>
        <div class="large-bar large-chart">
          <div class="large-title">项目产值</div>
          <bar-chart />
        </div>
        <div class="large-pie large-chart">
          <div class="large-title">人员与安全（今日）</div>
          <div class="pieChart">
            <pie-chart
              name="人员"
              unit="人"
              :legend-data="['在岗人员', '离岗人员']"
              :series-data="['89', '6']"
            />
            <pie-chart
              name="安全事件"
              unit="件"
              :legend-data="['已处理', '待处理']"
              :series-data="['45', '19']"
            />
          </div>
        </div>
      </div>
      <div class="large-center">
        <div class="large-img">
          <div class="large-item">
            <p>
              <img :src="srcGlobel" alt>
              <img :src="srcInternational" alt>
            </p>
            <div class="large-number">
              <div v-for="(item,index) in internationalNum" :key="index">
                <div />
                <div />
                <span>{{ item }}</span>
              </div>
            </div>
          </div>
          <div class="large-item">
            <p>
              <img :src="srcChinaMap" alt>
              <img :src="srcdDomestic" alt>
            </p>
            <div class="large-number">
              <div v-for="(item,index) in domesticlNum" :key="index">
                <div />
                <div />
                <span>{{ item }}</span>
              </div>
            </div>
          </div>
        </div>
        <div class="GlobeChart">
          <globe-chart />
        </div>
      </div>
      <div class="large-right large-chart">
        <div class="large-title">集团公司</div>
        <collapse />
      </div>
    </div>
  </div>
</template>

<script>
import barChart from './components/barChart'
import pieChart from './components/pieChart'
import globeChart from './components/globeChart'
import collapse from './components/collapse'
import moment from 'moment'
moment.locale('zh-cn')
export default {
  name: 'Large',
  components: {
    barChart,
    pieChart,
    globeChart,
    collapse
  },
  data() {
    return {
      itemImg: require('@/assets/images/project.png'),
      srcName: require('@/assets/images/bg_name.png'),
      srcInternational: require('@/assets/images/international.png'),
      srcdDomestic: require('@/assets/images/domestic.png'),
      srcGlobel: require('@/assets/images/globel.png'),
      srcChinaMap: require('@/assets/images/ChinaMap.png'),
      time: moment().format('YYYY-MM-DD HH:mm dddd'),
      timer: null,
      address: '南京市雨花台区',
      internationalNum: ['2', '5', '6'],
      domesticlNum: ['4', '1', '0'],
      underNum: ['2', '1', '4']
      // legendData:[]
    }
  },
  created() {
    this.init()
  },
  destroyed() {
    clearInterval(this.timer)
  },
  methods: {
    init() {
      this.timer = setInterval(() => {
        this.time = moment().format('YYYY-MM-DD HH:mm dddd')
      }, 1000)
    }
  }
}
</script>

<style lang="scss" scoped>
@import "~@/assets/font/font.scss";
.large-container {
  background: url("~@/assets/images/bg.png");
  background-size: 100% 100%;
  background-repeat: no-repeat;
  height: 100%;
  .large-name {
    text-align: center;
    margin: 0 auto;
    position: relative;
    padding-top: 0.5%;
    img {
      width: 153px;
    }
    span {
      color: #90d1ff;
      font-size: 12px;
      position: absolute;
      bottom: -30%;
    }
    .large-time {
      left: 10%;
    }
    .large-address {
      right: 10%;
    }
  }
  .large-content {
    display: flex;
    height: 85%;
    width: 90%;
    margin: 2% auto 0;
    color: #ffffff;
    .large-left {
      width: 28%;
      .large-left-num {
        height: 14%;
        width: 80%;
        margin: 0 auto;
        display: flex;
        justify-content: center;
        background: url("~@/assets/images/baseImg.png");
        background-repeat: no-repeat;
        background-position: center bottom;
        position: relative;
        & > div {
          width: 20%;
          height: 65%;
          font-size: 50px;
          color: #ffbe60;
          display: flex;
          justify-content: center;
          align-items: center;
          border: 1px solid rgba(5, 117, 164, 1);
          border-radius: 2px;
          margin: 0 5px;
          background: rgba(60, 202, 255, 0.1);
          font-family: DS-DIGIB-2;
        }
        p {
          position: absolute;
          bottom: 0;
          left: 0;
          right: 0;
          margin: 0 auto;
          margin: 0;
          line-height: 26px;
          text-align: center;
          img {
            vertical-align: middle;
          }
        }
      }
      .large-bar {
        height: 45%;
        width: 100%;
      }
      .large-pie {
        height: 40%;
        width: 100%;
        .pieChart {
          display: flex;
          width: 100%;
          height: 80%;
          & > div {
            width: 50%;
          }
        }
      }
    }
    .large-center {
      width: 47%;
      .large-img {
        width: 100%;
        display: flex;
        justify-content: center;
        & > div:first-child {
          margin-right: 10%;
        }
        .large-item {
          p {
            display: flex;
            margin: 0;
          }
          .large-number {
            display: flex;
            justify-content: center;
            font-size: 50px;
            color: #ffffff;
            font-family: DS-DIGIB-2;
            & > div {
              position: relative;
              width: 46px;
              height: 65px;
              margin: 0 5px;
              & > div {
                width: 100%;
                height: 29px;
                background-color: rgba(27, 112, 228, 0.41);
              }
              & > div:first-child {
                margin-bottom: 2px;
              }
              span {
                position: absolute;
                left: 50%;
                top: 50%;
                transform: translate(-50%, -50%);
              }
            }
          }
        }
      }
      .GlobeChart {
        height: 85%;
        width: 100%;
        margin-top: 10px;
      }
    }
    .large-right {
      width: 25%;
      height: 100%;
      background: url("~@/assets/images/bg_right.png");
    }
    .large-chart {
      background: url("~@/assets/images/frame.png");
      background-size: 100% 100%;
      background-repeat: no-repeat;
      margin-top: 5px;
      padding: 10px;
      color: #00d2ff;
      font-size: 14px;
      .large-title {
        width: 100%;
        line-height: 36px;
        padding-left: 20px;
        background: url("~@/assets/images/bg_title.png");
        background-size: 70% 100%;
        background-repeat: no-repeat;
      }
    }
  }
}
</style>
