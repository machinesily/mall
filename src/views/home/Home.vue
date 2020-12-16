<template>
  <div id="home">
    <nav-bar class="home-nav">
      <!-- 顶部导航 -->
      <div slot="center">购物街</div>
    </nav-bar>
    <home-swiper :banners="banners"></home-swiper><!-- 轮播图 -->
    <home-recommend :recommends="recommends"></home-recommend><!-- 推荐 -->
    <feature-view /><!-- 本周流行（图片） -->
    <tab-control class="tabcontrol" :titles="['流行','新款','精选']" @tabClick="tabClick" />
    <goods-list :goods="this.goods[currentType].list" />
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
  import GoodsList from '../../components/content/goodsList/GoodsList.vue'


  //导入的方法
  import {
    getHomeMultidata,
    getGoodsData
  } from 'network/home'

  export default {
    components: {
      NavBar,
      HomeSwiper,
      HomeRecommend,
      FeatureView,
      TabControl,
      GoodsList,
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
        })
      }
    }
  }
</script>

<style>
  .home-nav {
    background-color: var(--color-tint);
    color: white;
  }

  img {
    width: 100%;
  }

  #home {
    padding-top: 44px;
    /*顶部导航的高度*/
  }

  .tabcontrol {
    position: sticky;
    /*定位*/
    top: 44px
      /*顶部导航的高度*/
  }
</style>