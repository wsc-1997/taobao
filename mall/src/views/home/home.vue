<template>
  <div id="home">
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
    <tab-control class="tab-control"
                 :title="['流行','新款','精选']"
                 @tabClick="tabclick"
                 ref="tabcontrol1"
                 v-show="istabshow"></tab-control>
    <Scroll class="contents"
            ref="scroll"
            :probe-type="3"
            :pull-up-load="true"
            @scroll="contentscroll"
            @pullingUp="loadmore">
      <homeswiper :data="banner" @load="swiperomgload"></homeswiper>
      <home-recommend-view :recommends="recommends"></home-recommend-view>
      <feature-view></feature-view>
      <tab-control :title="['流行','新款','精选']"
                   @tabClick="tabclick"
                   ref="tabcontrol2"></tab-control>
      <goods :goods="showgoods"></goods>
    </Scroll>
    <backtop @click.native="backclick" v-show="isshow"></backtop>
  </div>
</template>

<script>
import homeswiper from "@/views/home/childcomps/homeswiper";
import homeRecommendView from "@/views/home/childcomps/homeRecommendView";
import FeatureView from "@/views/home/childcomps/FeatureView";


import backtop from "@/components/content/backtop/backtop";
import NavBar from "@/components/common/navbar/NavBar";
import TabControl from "@/components/content/tabControl/TabControl";
import goods from "@/components/content/goods/goods";
import Scroll from "@/components/common/scroll/Scroll";

import {getHomeMultidata,getHomeGoods} from "@/network/home";
import Goods from "@/components/content/goods/goods";



export default {
  name: "home",
  components: {
    Goods,
    NavBar,
    homeswiper,
    homeRecommendView,
    FeatureView,
    TabControl,
    goods,
    Scroll,
    backtop
  },
  data() {
    return{
      banner:[],
      recommends:[],
      goods: {
        'pop':{page: 0,list:[]},
        'new':{page: 0,list:[]},
        'sell':{page: 0,list:[]},
      },
      currentType:'pop',
      isshow: false,
      taboffsettop: 0,
      istabshow: false,
      saveY: 0
    }
  },
  computed: {
    showgoods(){
      return this.goods[this.currentType].list
    }
  },
  activated() {
    this.$refs.scroll.scroll.refresh()
    this.$refs.scroll.scroll.scrollTo(0,this.saveY,0)
  },
  deactivated() {
    this.saveY = this.$refs.scroll.scroll.y
  },
  created() {
    this.getHomeMultidata()

    this.getHomegoods('pop')
    this.getHomegoods('new')
    this.getHomegoods('sell')
  },
  methods:{
    tabclick(index){
      switch (index){
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
      this.$refs.tabcontrol1.currentIndex = index
      this.$refs.tabcontrol2.currentIndex = index
    },
    backclick(){
      this.$refs.scroll.scroll.scrollTo(0,0,500)
    },
    contentscroll(position){
      this.isshow = (-position.y) > 500;
      this.istabshow = (-position.y) > this.taboffsettop;
    },


    /*数据请求*/
    getHomeMultidata(){
      getHomeMultidata().then(res =>{
        this.banner = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      })
    },
    getHomegoods(type){
      const page = this.goods[type].page + 1;
      getHomeGoods(type, page).then(res =>{
        this.goods[type].list.push(...res.data.list);
        this.goods[type].page += 1;
      })
    },
    loadmore(){
      this.getHomegoods(this.currentType);
      this.$refs.scroll.finishPullup();
    },
    swiperomgload(){
      this.taboffsettop = this.$refs.tabcontrol2.$el.offsetTop;
    }
  }
}
</script>

<style scoped>
#home{
  position: relative;
  height: 100vh;
}

.home-nav{
  background-color: var(--color-text);
  color: #fff;

  /*position: fixed;*/
  /*left: 0;*/
  /*right: 0;*/
  /*top: 0;*/
  /*z-index: 9;*/

}
.tab-control{
  position: relative;
  z-index: 9;
}
.contents{
  position: absolute;
  overflow: hidden;
  top:44px ;
  left: 0;
  right: 0;
  bottom: 49px;
}
.tableshow{

}
</style>