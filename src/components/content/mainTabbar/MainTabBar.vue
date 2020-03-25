<template>
  <div>
    <tab-bar >
      <tab-bar-item path="/home" activeColor="#faa">
          <img slot="item-icon" src="~assets/img/tabbar/home.png" alt="">
          <img slot="item-icon-active" src="~assets/img/tabbar/home@selected.png" alt="">
          <div slot="item-text">首页</div>
      </tab-bar-item>
      <tab-bar-item path="/profile" activeColor="#faa">
          <img slot="item-icon" src="~assets/img/tabbar/my.png" alt="">
          <img slot="item-icon-active" src="~assets/img/tabbar/my@selected.png" alt="">
          <div slot="item-text">我的</div>
      </tab-bar-item>
      <tab-bar-item path="/cart" activeColor="#faa">
          <img slot="item-icon" src="~assets/img/tabbar/cart.png" alt="">
          <img slot="item-icon-active" src="~assets/img/tabbar/cart@selected.png" alt="">
          <div slot="item-text">购物车</div>
      </tab-bar-item>
      <tab-bar-item path="/category" activeColor="#faa">
          <img slot="item-icon" src="~assets/img/tabbar/category.png" alt="">
          <img slot="item-icon-active" src="~assets/img/tabbar/category@selected.png" alt="">
          <div slot="item-text">分类</div>
      </tab-bar-item>
    </tab-bar>
  </div>
</template>
<script>
import TabBar from 'components/common/tabbar/TabBar.vue'
import TabBarItem from 'components/common/tabbar/TabBarItem.vue'
export default {
  name: 'MainTabBar',
  components: {
    TabBar,
    TabBarItem
  }
}

</script>
<style>

</style>
