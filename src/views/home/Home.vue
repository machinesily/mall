<template>
  <div id="home" class="wrapper">
    <!-- 顶部导航 -->
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
    <tab-control class="tab-control" v-show="tabFixed" :titles="['流行','新款','精选']" @tabClick="tabClick" ref="tabContorl1"/>
    <scroll class="content" ref="scroll" :probeType="3" @scrollPosition='scrollPosition' :pullUpLoad="true"
      @pullingUp='loadMore'>
      <!--滚动组件-->
      <home-swiper :banners="banners" @swiperImgLoad="swiperImgLoad"/><!-- 轮播图 -->
      <home-recommend :recommends="recommends"></home-recommend><!-- 推荐 -->
      <feature-view /><!-- 本周流行（图片） -->
      <tab-control :titles="['流行','新款','精选']" @tabClick="tabClick" ref="tabContorl2"/>
      <goods-list :goods="this.goods[currentType].list" /><!-- 商品展示 -->
    </scroll>
    <back-top @click.native="backTopClick" v-show="isShowBackTop" />
    <!--返回顶部-->
  </div>
</template>

<script>
  //导入的子组件
  import HomeSwiper from './homeComps/homeSwiper.vue'
  import HomeRecommend from './homeComps/homeRecommend.vue'
  import FeatureView from './homeComps/FeatureView.vue'
  import BackTop from '../../components/content/backTop/BackTop.vue'


  //导入的公共组件
  import NavBar from 'components/common/navbar/NavBar.vue'
  import TabControl from '../../components/content/tabControl/TabControl.vue'
  import GoodsList from '../../components/content/goodsList/GoodsList.vue'
  import Scroll from '../../components/common/scroll/Scroll.vue'


  // 导入的方法
  import {
    getHomeMultidata,
    getGoodsData
  } from 'network/home'
  // 防抖方法
  import {
    debounce
  } from 'common/JS/debounce'


  export default {
    components: {
      NavBar,
      HomeSwiper,
      HomeRecommend,
      FeatureView,
      TabControl,
      GoodsList,
      Scroll,
      BackTop,
    },
    data() {
      return {
        banners: [],
        recommends: [],
        goods: {
          'pop': {
            page: 0,
            list: []
          },
          'new': {
            page: 0,
            list: []
          },
          'sell': {
            page: 0,
            list: []
          }
        },
        currentType: 'pop',
        isShowBackTop: false,
        tabOffsetTop: 0,
        tabFixed:false
      }
    },
    created() {
      //请求轮播图的数据
      this.getHomeMultidata()
      //请求商品数据
      this.getGoodsData('pop')
      this.getGoodsData('new')
      this.getGoodsData('sell')
    },
    mounted() {
      //监听item图片加载完成
      const refresh = debounce(this.$refs.scroll.refresh, 200)
      this.$bus.$on('itemImageLoad', _ => {
        refresh()
      })
    },
    methods: {
      //事件监听的方法
      tabClick(index) {
        switch (index) {
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
        this.$refs.tabContorl1.currentIndex = index
        this.$refs.tabContorl2.currentIndex = index
      },
      //返回顶部的方法
      backTopClick() {
        this.$refs.scroll.scrollTo(0, 0, 1000)
      },
      //实时监听滚动位置
      scrollPosition(position) {
        // 1.判断BackTop是否显示
        this.isShowBackTop = (-position.y) > 1000

        // 2.判断tabControl是否吸顶
        this.tabFixed = (-position.y) > this.tabOffsetTop
      },

      //上拉加载更多的方法
      loadMore() {
        this.getGoodsData(this.currentType)
      },

      swiperImgLoad() {
        this.tabOffsetTop = this.$refs.tabContorl2.$el.offsetTop;
      },

      //网络请求的方法
      getHomeMultidata() {
        getHomeMultidata().then(res => {
          // console.log(res);
          this.banners = res.data.data.banner.list
          this.recommends = res.data.data.recommend.list
        })
      },
      getGoodsData(type) {
        const page = this.goods[type].page + 1
        getGoodsData(type, page).then(res => {
          // console.log(res.data.data);
          // for (let list of res.data.data.list) {  //使用遍历的方法
          //   this.goods[type].list.push(list)
          // }
          this.goods[type].list.push(...res.data.data.list) //把请求过来的数据插入到Home.vue中保存
          this.goods[type].page += 1
          this.$refs.scroll.finishPullUp()
        })
      }
    }
  }
</script>

<style scoped>
  .home-nav {
    background-color: var(--color-tint);
    color: white;
  }

  img {
    width: 100%;
  }

  #home {
    height: 100vh;
    position: relative;
    /*顶部导航的高度*/
  }

  .content {
    position: absolute;
    overflow: hidden;
    top: 44px;
    left: 0;
    right: 0;
    bottom: 49px;
  }

  .tab-control{
    position: relative;
  }
</style>