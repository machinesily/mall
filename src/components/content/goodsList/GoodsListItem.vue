<template>
  <div class="goods-item" @click="goodsClick">
    <img :src="goodsItem.show.img" alt="" @load="imageLoad">
    <div class="goods-info">
      <p>{{goodsItem.title}}</p>
      <span class="prise">{{goodsItem.price}}</span>
      <span class="collect">{{goodsItem.cfav}}</span>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      goodsItem: {
        type: Object,
        default: {}
      }
    },
    methods:{
      //监听图片加载完成，发送事件总线
      imageLoad() {
        this.$bus.$emit('itemImageLoad')
      },

      goodsClick(){
        // 跳转到详情页
        this.$router.push('detail/'+this.goodsItem.iid)
      }
    }
  }
</script>

<style>
  .goods-item {
    width: 48%;
    position: relative;
    padding-bottom: 40px;
  }

  .goods-item img {
    width: 100%;
    border-radius: 5px;
  }

  .goods-info {
    font-size: 12px;
    position: absolute;
    bottom: 5px;
    left: 0;
    right: 0;
    overflow: hidden;
    text-align: center;
  }

  .goods-info p {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    margin-bottom: 3px;
  }

  .goods-info .prise {
    color: var(--color-high-text);
    /* position: relative;
    right:20px; */
    margin-right: 20px;
  }

  .goods-info .collect {
    position: relative;
  }

  .goods-info .collect::before {
    content: '';
    position: absolute;
    left: -15px;
    top: -1px;
    width: 14px;
    height: 14px;
    background: url("~assets/img/common/collect.svg") 0 0/14px 14px;
  }
</style>