<template>
  <tabbar>
    <tabbar-item>
      <img slot="icon" src="../assets/dot.png">
      <span slot="label">Wechat</span>
    </tabbar-item>
    <tabbar-item>
      <img slot="icon" src="../assets/book.png">
      <span slot="label">Message</span>
    </tabbar-item>
    <tabbar-item>
      <img slot="icon" src="../assets/menu.png">
      <span slot="label">News</span>
    </tabbar-item>
  </tabbar>
</template>

<script>
import { Tabbar, TabbarItem, AjaxPlugin } from 'vux'
export default {
  components: {
    Tabbar,
    TabbarItem,
    AjaxPlugin
  }
}
</script>

<style>
</style>