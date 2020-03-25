<template>
  <div id="home">
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
    <scroll class="content" 
    @scroll="contentScroll"
     @loadMore="loadMore" ref="scroll"
     :pull-up-load="true"
      :probe-type="0">
      <home-swiper :banners="banners" />  
      <recommend-view :recommends="recommends" />
      <feature/>
      <tab-control @tabClick="tabClick" class="tab-control" :titles="titles" />
      <goods-list :good-list="goodsType" />
    </scroll>
    <back-top v-show="isShowBackTop" @click.native="backTop" class="back-top" />
    <!-- 监听原生组件的事件 -->
  </div>
</template>
<script>
import HomeSwiper from './childComps/HomeSwiper'
import RecommendView from './childComps/RecommendView'
import Feature from './childComps/Feature'

import NavBar from 'components/common/navbar/NavBar'
import TabControl from 'components/content/tabControl/TabControl'
import GoodsList from 'components/content/goods/GoodsList'
import Scroll from 'components/common/scroll/Scroll'
import BackTop from 'components/content/backTop/BackTop'

import { getmultidata, getHomeGoods } from 'network/home'
export default {
  name: 'Home',
  components: {
    HomeSwiper,
    RecommendView,
    Feature,
    NavBar,
    TabControl,
    GoodsList,
    Scroll,
    BackTop
  },
  data () {
    return {
      banners: [],
      recommends: [],
      titles: ['流行', '新品', '精选'],
      goods: {
        pop: {page: 0, list: []},
        new: {page: 0, list: []},
        sell: {page: 0, list: []}
      },
      currentType: 'pop',
      isShowBackTop: false
    }
  },
  computed: {
    goodsType (){
      return this.goods[this.currentType].list
    }
  },
  created () {
    this.getmultidata()
    this.getHomeGoods('pop')
    this.getHomeGoods('new')
    this.getHomeGoods('sell')    
  },
  mounted () {
    
  },
  methods: {
    /*
    * 事件监听相关方法
    */
    tabClick (index) {
      switch(index) {
        case 0: 
          this.currentType = 'pop'
          break
        case 1: 
          this.currentType = 'new'
          break
        case 2: 
          this.currentType = 'sell'
          break
      }
    },
    contentScroll (position) {
      this.isShowBackTop = (-position.y) > 1000
      // document.getElementsByClassName('back-top').style.display = position.y < -2000 ? 'block' : 'none';
      // 繁琐写法：
      // this.isShowBackTop = -position.y > 1000 ? true : false
      // 错误写法：
      // if (-position.y > 1000) {
      //   this.isShowBackTop = true
      // }
    },
    loadMore () {
      this.getHomeGoods(this.currentType)      
    },
  /*
   * 网络请求相关方法
   */
    getmultidata () {
      getmultidata().then(res => {
        this.banners = res.data.banner.list
        this.recommends = res.data.recommend.list
      }, err => console.log(err))
    },
    getHomeGoods (type) {
      let page = this.goods[type].page + 1
      getHomeGoods(type, page).then(res => {
        this.goods[type].list.push(...res.data.list)
        this.goods[type].page += 1
      })
    },
    /*
    * 普通方法
   */
    backTop () {
      this.$refs.scroll.scrollTo(0, 0, 500)
    }
  }
}
</script>
<style scoped>
  #home {
    height: 100vh;
    /* vh: viewport height 视口 */
    padding-top: 44px;
    position: relative;
  }
  .home-nav {
    background-color: var(--color-tint);
      color: #fff;
    position: fixed;
    left: 0;
    top: 0;
    right: 0;
    z-index: 9;
  }
  .tab-control {
    background-color: #fff;
    position: sticky;
    top: 44px;
    z-index: 9;
  }

  .content {
    /* height: calc(100% - 93px);
    margin-top: 44px; */
    position: absolute;
    top: 44px;
    bottom: 49px;
  }
  /* 瀑布流 */
</style>
