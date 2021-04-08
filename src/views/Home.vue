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
          <div :class="[{activeStart: startId == v.id}, {activeEnd: endId == v.id}, 'box']" @click="chooseImg(v, index)">
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
    end: null // 结束那项的id
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
    chooseImg (v, index) {
      console.log('index===========================')
      console.log(index)
      console.log('start===========================')
      console.log(this.start)
      console.log('end=============================')
      console.log(this.end)
      // 点击开始
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
      console.log(v, index)
      this.startId = v.id
      this.start = index
    },
    // 选择结束图片
    chooseEndImg (v, index) {
      console.log(v, index)
      this.endId = v.id
      this.end = index
    },
    // 重置选择结果
    resetChoose (v, index) {
      console.log('重置')
      this.start = null
      this.end = null
      this.startId = ''
      this.endId = ''
      this.chooseImg(v, index)
    },
    // 确定
    sub () {
      console.log('start================================')
      console.log(this.start)
      console.log('end==================================')
      console.log(this.end)
      var arr = this.imgs.slice(this.start, this.end + 1)
      console.log('选中的数组=====================================')
      console.log(arr)
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
</style>