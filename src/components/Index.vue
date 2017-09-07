<template>
  <div>
  	<x-header :left-options="{showBack: false}">首页</x-header>
  	<swiper loop auto :list="demo03_list" :index="demo06_index" @on-index-change="demo06_onIndexChange"></swiper>
  	<!--
   	<group>
      <cell title="title" value="value"></cell>
    </group>
  	-->
  </div>
</template>

<script>
import { AjaxPlugin, XHeader, Swiper, Group, Cell } from 'vux'

const imgList = [
  'http://placeholder.qiniudn.com/800x300/FF3B3B/ffffff'
]

const demoList = imgList.map((one, index) => ({
  url: 'javascript:',
  img: one
}))

export default {
  components: {
    AjaxPlugin,
    XHeader,
    Swiper,
    Group,
    Cell
  },
  created: function () {
    let _this = this
    getRequest('http://image.nebulous.cn/v1/image/list', function (data) {
      let a = data.map((image, index) => ({
        url: 'javascript:',
        img: 'http://' + image.imageUrl
      }))
      _this.demo03_list = a
    })
  },
  methods: {
    demo06_onIndexChange (index) {
      this.demo06_index = index
    }
  },
  data () {
    return {
      demo03_list: demoList,
      demo06_index: 0
    }
  }
}

function getRequest (url, cb) {
  AjaxPlugin.$http.get(url)
  .then((response) => {
    if (cb) cb(response.data)
  })
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
