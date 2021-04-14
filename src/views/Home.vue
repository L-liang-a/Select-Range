<template>
  <div>
    <img alt="Vue logo" src="../assets/logo.png">
    <a-row>
      <template v-for="(v,index) in imgs">
        <a-col
          class="card"
          :key="index"
          :sm="8"
          :md="6"
          :lg="4"
          :xl="2">
          <div :class="[{activeStart: startId == v.id}, {activeEnd: endId == v.id}, 'box', setClass(v)]" @click="chooseImg(v, index)">
            {{ v.url }}
          </div>
        </a-col>
      </template>
      <a-button @click="sub">确定</a-button>
    </a-row>
  </div>
</template>

<script>
export default {
name: 'home',
components: {},
props: {},
data () {
  return {
    imgs: [],
    startId: '', // 开始那项的id
    endId: '', // 结束那项的id
    start: null, // 开始那项的索引
    end: null, // 结束那项的id
    chooseImgs: [], // 选中的数组
    clickMid: false, // 判断选中的区间再次点击是否为区间内的中间区域
  }
},
computed: {},
watch: {},
mounted () {},
created () {
  var arr = []
  for (let i = 1; i < 27; i++) {
    arr.push({ url: String(i), id: i + 1 })
  }
  this.imgs = arr
},
methods: {
    // 动态添加class属性
    setClass (v) {
      if (this.chooseImgs.length > 0) {
        // 判断如果选中的数组和v-for遍历出来的数组id一致就给他添加遮罩
        for (let i = 0; i < this.chooseImgs.length; i++) {
          if (this.chooseImgs[i].id === v.id) {
            return 'popContainer'
          }
        }
      } else {
        return ''
      }
    },
    chooseImg (v, index) {
      console.log('index===========================')
      console.log(index)
      console.log('start===========================')
      console.log(this.start)
      console.log('end=============================')
      console.log(this.end)
      // // 拓展
      // if ((this.start !== null && this.end !== null) && (index > this.start && index < this.end)) {
      //   this.clickMid = true
      // }
      // // 点击开始
      // if ((this.start === null && this.end === null) || (this.start !== null && index < this.start)) {
      //   this.chooseStartImg(v, index)
      // } else if (this.start !== null && this.end === null && index > this.start) { // 点击结束
      //   this.chooseEndImg(v, index)
      // } else if (this.start !== null && this.end !== null && (index > this.end || index > this.start) && !this.clickMid) {
      //   this.chooseEndImg(v, index)
      // } else if (index === this.start || this.clickMid) { // 如果当前选中的index等于开始的index就重置为开始选择
      //   this.resetChoose(v, index)
      // } else {
      //   this.resetChoose(v, index)
      // }
      if ((this.start === null && this.end === null)) {
        console.log('点击开始')
        this.chooseStartImg(v, index)
      } else if (this.start !== null && this.end === null && index > this.start) { // 点击结束
        console.log('点击结束')
        this.chooseEndImg(v, index)
      } else if (this.start !== null && this.end !== null) {
        this.resetChoose(v, index)
      } else if (index === this.start) { // 如果当前选中的index等于开始的index就重置为开始选择
        this.resetChoose(v, index)
      } else {
        this.resetChoose(v, index)
      }
    },
    // 选择开始图片
    chooseStartImg (v, index) {
      console.log('点击开始')
      console.log(v, index)
      this.startId = v.id
      this.start = index
      // 拓展功能时解开
      // if (this.start !== null && this.end !== null) {
      //   this.chooseImgs = this.imgs.slice(this.start, this.end + 1);
      // }
    },
    // 选择结束图片
    chooseEndImg (v, index) {
      console.log('点击结束')
      console.log(v, index)
      this.endId = v.id
      this.end = index
      if (this.start !== null && this.end !== null) {
        this.chooseImgs = this.imgs.slice(this.start, this.end + 1)
      }
    },
    // 重置选择结果
    resetChoose (v, index) {
      console.log('重置')
      this.start = null
      this.end = null
      this.startId = ''
      this.endId = ''
      this.chooseImgs = []
      this.clickMid = false
      this.chooseImg(v, index)
    },
    // 确定
    sub () {
      console.log('start================================')
      console.log(this.start)
      console.log('end==================================')
      console.log(this.end)
      if (this.start === null) {
        this.$message.error('请选择开始节点')
      } else if (this.end === null) {
        this.$message.error('请选择结束节点')
      } else {
        var arr = this.imgs.slice(this.start, this.end + 1)
        console.log('选中的数组=====================================')
        console.log(arr)
      }
    }
  }

}
</script>

<style lang='less' scoped>
.card {
  margin: 10px;
}
.box {
  background: pink;
  width: 100px;
  height: 100px;
  margin: 0 auto;
  font-size: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
}
.activeStart {
  border: 2px solid green;
}
.activeEnd {
  border: 2px solid red;
}
.popContainer{
  // position: fixed;
  // top: 0;
  // left: 0;
  // right: 0;
  // bottom: 0;
  // z-index: 999;
  background: rgba(0,0,0,0.3);
}
</style>