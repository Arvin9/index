<template>
  <div>
  	<x-header :left-options="{showBack: false}">首页</x-header>
  	<swiper loop auto :list="demo03_list" :index="demo06_index" @on-index-change="demo06_onIndexChange"></swiper>
  	<!--
   	<group>
      <cell title="title" value="value"></cell>
    </group>
  	-->
    <checklist :label-position="labelPosition" required :options="commonList" v-model="checkList" @on-change="change">
    </checklist>
  	
  
  	<Foot></Foot>  
  </div>
</template>

<script>
import { Checklist, AjaxPlugin, XHeader, Swiper, Group, Cell } from 'vux'
import Foot from './Footer'

const imgList = [
]

const demoList = imgList.map((one, index) => ({
  url: 'javascript:',
  img: one
}))

export default {
  components: {
    Checklist,
    AjaxPlugin,
    XHeader,
    Swiper,
    Group,
    Cell,
    Foot
  },
  created: function () {
    let _this = this
    let params = {
      imageCategory: 10
    }
    postRequest('http://www.abner.top/v1/images/list', params, function (data) {
      let a = data.map((image, index) => ({
        url: 'javascript:',
        img: image.imageUrl
      }))
      _this.demo03_list = a
    })
  },
  methods: {
    demo06_onIndexChange (index) {
      this.demo06_index = index
    },
    change (val) {
      this.$data.commonList = sort(this.$data.checkList, this.$data.commonList)
    }
  },
  data () {
    return {
      demo03_list: demoList,
      demo06_index: 0,
      labelPosition: '',
      checkList: [],
      commonList: [ {key: '1', value: 'China'}, {key: '2', value: 'America'} ]
    }
  }
}

/**
 * 排序
 * 遍历
 */
function sort (checkList, commonList) {
  var arr1 = []
  var arr2 = []
  var flag = false
  for (let i = 0; i < commonList.length; i++) {
    flag = false
    for (let j = 0; j < checkList.length; j++) {
      if (commonList[i].key === checkList[j]) {
        arr2.push(commonList[i])
        flag = true
      }
    }
    if (!flag) {
      arr1.push(commonList[i])
    }
  }
  return arr1.concat(arr2)
}

function postRequest (url, params, cb) {
  AjaxPlugin.$http.post(url, params)
  .then((response) => {
    if (cb) cb(response.data)
  })
}
/*
function getRequest (url, cb) {
  AjaxPlugin.$http.get(url)
  .then((response) => {
    if (cb) cb(response.data)
  })
}
*/
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.weui-tabbar__label {
	margin: 0px;
}
a:-webkit-any-link {
	text-decoration: none;
}
</style>
