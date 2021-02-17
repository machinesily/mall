<template>
  <div id="detail">
    <detail-nav-bar class="detail-nav" />
    <scroll class="content" ref="scroll">
        <detail-swiper :top-images="topImages" :probe-type="3" />
        <detail-base-info :goods="goods" />
        <detail-shop-info :shop="shop" />
        <detail-goods-info :detailInfo="detailInfo" @imageLoad="imageLoad" />
    </scroll>
  </div>
</template>

<script>
  import detailNavBar from './childComps/DetailNavBar.vue'
  import detailSwiper from './childComps/DetailSwiper'
  import detailBaseInfo from './childComps/DetailBaseInfo'
  import detailShopInfo from './childComps/DetailShopInfo'
  import Scroll from '../../components/common/scroll/Scroll.vue'
  import detailGoodsInfo from './childComps/DetailGoodsInfo'


  import {
    getDetail,
    Goods,
    Shop
  } from 'network/detail'
  export default {
    name: 'Detail',
    components: {
      detailNavBar,
      detailSwiper,
      detailBaseInfo,
      detailShopInfo,
      Scroll,
      detailGoodsInfo
    },
    data() {
      return {
        id: null,
        topImages: [],
        goods: {},
        shop: {},
        detailInfo: {}
      }
    },
    created() {
      // 保存传过来的id
      this.id = this.$route.params.id
      // 发送网络请求
      getDetail(this.id).then(res => {
        let data = res.data.result
        // 获取轮播图图片
        this.topImages = data.itemInfo.topImages

        // 获取商品数据
        this.goods = new Goods(data.itemInfo, data.columns, data.shopInfo.services)

        // 获取商店信息
        this.shop = new Shop(data.shopInfo)

        // 获取商品详情页
        this.detailInfo = data.detailInfo
        
      })
    },
    methods: {
      imageLoad() {
        this.$refs.scroll.refresh()
      }
    },
  }
</script>

<style scoped>
  #detail {
    background-color: #fff;
    position: relative;
    z-index: 9;
    height: 100vh;
  }

  .detail-nav {
    position: relative;
    z-index: 9;
    background-color: #fff;
  }

  .content {
    height: calc(100% - 44px);
  }
</style>