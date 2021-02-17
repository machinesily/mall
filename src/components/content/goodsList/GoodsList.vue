<template>
  <div class="goodslist">
    <goods-list-item v-for="item in goods" :key="item.index" :goodsItem="item"/>
  </div>
</template>

<script>
  import GoodsListItem from './GoodsListItem.vue'
  export default {
    components: {
      GoodsListItem
    },
    props: { //从Home.vue传过来的数据保存
      goods: {
        type: Array,
        default: []
      }
    }
  }
</script>

<style>
.goodslist{
  display: flex;
  justify-content: space-evenly;
  flex-wrap: wrap;
}
</style>