<template>
  <div id="home">
    <nav-bar class="home-nav"><!-- 顶部导航 -->
      <div slot="center">购物街</div>
    </nav-bar>
    <home-swiper :banners="banners"></home-swiper><!-- 轮播图 -->
    <home-recommend :recommends="recommends"></home-recommend><!-- 推荐 -->
    <feature-view /><!-- 本周流行（图片） -->
    <tab-control class="tabcontrol" :titles="['流行','新款','精选']"/>
    <ui>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
    </ui>
  </div>
</template>

<script>
  //导入的子组件
  import HomeSwiper from './homeComps/homeSwiper.vue'
  import HomeRecommend from './homeComps/homeRecommend.vue'
  import FeatureView from './homeComps/FeatureView.vue'

  //导入的公共组件
  import NavBar from 'components/common/navbar/NavBar.vue'
  import TabControl from '../../components/content/tabControl/TabControl.vue'

  //导入的方法
  import {getHomeMultidata} from 'network/home'

  export default {
    components: {
      NavBar,
      HomeSwiper,
      HomeRecommend,
      FeatureView,
      TabControl,
    },
    data() {
      return {
        banners: [],
        recommends: []
      }
    },
    created() {
      getHomeMultidata().then(res => {
        console.log(res);
        this.banners = res.data.data.banner.list
        this.recommends = res.data.data.recommend.list
      })
    },
  }
</script>

<style>
  .home-nav {
    background-color: var(--color-tint);
    color: white;
  }
  img{
    width: 100%;
  }
  #home{
    padding-top: 44px; /*顶部导航的高度*/
  }

  .tabcontrol{
    position: sticky; /*定位*/
    top:44px /*顶部导航的高度*/
  }
</style>