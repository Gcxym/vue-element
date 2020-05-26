<template>
  <div class="collapse">
    <div class="collapse-search">
      <el-input v-model="input" placeholder="请输入公司名称/项目名称" @input="handleSearch">
        <i slot="prefix" class="el-input__icon el-icon-search" />
      </el-input>
    </div>
    <div class="collapse-content">
      <div v-for="(item,index) in dataList" :key="index" class="numberItem">
        <div class="sectionItem" @click="showHide($event, item)">
          <p>
            <i class="el-icon-caret-right" :class="{rotate:item.isShow}" />
            <span>{{ item.company }}</span>
          </p>
        </div>
        <div class="pointItem">
          <el-collapse-transition>
            <div v-show="item.isShow">
              <p v-for="(cell,i) in item['itemList']" :key="i">
                <span>{{ cell.project }}</span>
              </p>
            </div>
          </el-collapse-transition>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Collapse',
  data() {
    return {
      input: '',
      dataList: [],
      totalList: [
        {
          company: '南京城建高淳投资有限公司',
          isShow: false,
          itemList: [
            { project: '城建智慧工地项目' },
            { project: '中江集团智慧工地项目' },
            { project: '城建智慧工地项目' },
            { project: '中江集团智慧工地项目' },
            { project: '城建智慧工地项目' }
          ]
        },
        {
          company: '南京城建高淳投资城建高淳投资有限公司',
          isShow: false,
          itemList: [
            { project: '城建智慧工地项目' },
            { project: '中江集团智慧工地项目' },
            { project: '城建智慧工地项目' },
            { project: '中江集团智慧工地项目' },
            { project: '城建智慧工地项目' }
          ]
        },
        {
          company: '南京城建高淳投资城建高淳投资有限公司',
          isShow: false,
          itemList: [
            { project: '城建智慧工地项目' },
            { project: '中江集团智慧工地项目' },
            { project: '城建智慧工地项目' },
            { project: '中江集团智慧工地项目' },
            { project: '城建智慧工地项目' }
          ]
        },
        {
          company: '南京城建高淳投资投投资资城建高淳投资有限',
          isShow: false,
          itemList: [
            { project: '城建智慧工地项目' },
            { project: '中江集团智慧工地项目' },
            { project: '城建智慧工地项目' },
            { project: '中江集团智慧工地项目' },
            { project: '城建智慧工地项目' }
          ]
        },
        {
          company: '南京城建高淳投资有限公司',
          isShow: false,
          itemList: [
            { project: '城建智慧工地项目' },
            { project: '中江集团智慧工地项目' },
            { project: '城建智慧工地项目' },
            { project: '中江集团智慧工地项目' },
            { project: '城建智慧工地项目' }
          ]
        },
        {
          company: '南京城建高淳投资有限公司',
          isShow: false,
          itemList: [
            { project: '城建智慧工地项目' },
            { project: '中江集团智慧工地项目' },
            { project: '城建智慧工地项目' },
            { project: '中江集团智慧工地项目' },
            { project: '城建智慧工地项目' }
          ]
        },
        {
          company: '南京城建高淳投资城建高淳投资有限公司',
          isShow: false,
          itemList: [
            { project: '城建智慧工地项目' },
            { project: '中江集团智慧工地项目' },
            { project: '城建智慧工地项目' },
            { project: '中江集团智慧工地项目' },
            { project: '城建智慧工地项目' }
          ]
        },
        {
          company: '南京城建高淳投资城建高淳投资有限公司',
          isShow: false,
          itemList: [
            { project: '城建智慧工地项目' },
            { project: '中江集团智慧工地项目' },
            { project: '城建智慧工地项目' },
            { project: '中江集团智慧工地项目' },
            { project: '城建智慧工地项目' }
          ]
        },
        {
          company: '南京城建高淳投资投投资资城建高淳投资有限',
          isShow: false,
          itemList: [
            { project: '城建智慧工地项目' },
            { project: '中江集团智慧工地项目' },
            { project: '城建智慧工地项目' },
            { project: '中江集团智慧工地项目' },
            { project: '城建智慧工地项目' }
          ]
        }
      ]
    }
  },
  mounted() {
    this.dataList = this.totalList
  },
  methods: {
    showHide(event, item) {
      item['isShow'] = !item['isShow']
      event.preventDefault()
      event.stopImmediatePropagation()
    },
    handleSearch() {
      const data = []
      this.totalList.forEach((item, index) => {
        if (item.company.indexOf(this.input) > -1) {
          data.push({
            company: item.company,
            isShow: false,
            itemList: item.itemList
          })
        }
        // else {
        //   const itemList = []
        //   item.itemList.forEach((cell, i) => {
        //     if (cell.project.indexOf(this.input) > -1) {
        //       itemList.push({
        //         project: cell.project
        //       })
        //     }
        //   })
        //   data.push({
        //     company: item.company,
        //     isShow: true,
        //     itemList: itemList
        //   })
        // }
      })
      if (data.length === 0) {
        this.totalList.forEach((item, index) => {
          const itemList = []
          item.itemList.forEach((cell, i) => {
            if (cell.project.indexOf(this.input) > -1) {
              itemList.push({
                project: cell.project
              })
            }
          })
          data.push({
            company: item.company,
            isShow: true,
            itemList: itemList
          })
        })
      }
      this.dataList = data
    }
  }
}
</script>

<style lang="scss" scoped>
.large-container {
  .large-chart {
    .collapse {
      width: 100%;
      height: calc(100% - 36px);
      padding: 0 10px;
      .collapse-content {
        height: calc(100% - 56px);
        overflow: hidden;
        overflow-y: auto;
        margin: 10px 0;
      }
      .numberItem {
        cursor: pointer;
        color: #b3ecff;
        line-height: 30px;
      }
      .sectionItem {
        p {
          line-height: 26px;
          margin: 0;
        }
        .rotate {
          transform: rotate(90deg);
        }
      }
      .pointItem {
        margin-left: 30px;
        color: #68cfff;
        p {
          line-height: 26px;
          margin: 0;
          position: relative;
          &::before {
            content: " ";
            position: absolute;
            left: -10px;
            top: 10px;
            width: 4px;
            height: 4px;
            background-color: #4ea5d1;
            border-radius: 4px;
          }
        }
      }
    }
  }
}
</style>
<style lang="scss">
.collapse {
  width: 100%;
  .collapse-search {
    .el-input__inner {
      border: none;
      color: #fff;
      background-color: rgba(66, 119, 254, 0.65);
      &::placeholder {
        color: #a8c0ec;
      }
    }
  }
  .collapse-content::-webkit-scrollbar {
    /*滚动条整体样式*/
    width: 5px; /*高宽分别对应横竖滚动条的尺寸*/
    height: 1px;
  }
  .collapse-content::-webkit-scrollbar-thumb {
    /*滚动条里面小方块*/
    border-radius: 20px;
    box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.2);
    background: #4a7390;
  }
  .collapse-content::-webkit-scrollbar-track {
    /*滚动条里面轨道*/
    box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.2);
    border-radius: 10px;
    background: rgba(0, 0, 0, 0);
  }
}
</style>
