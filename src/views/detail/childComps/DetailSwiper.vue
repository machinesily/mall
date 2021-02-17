<template>
  <div class="swiper">
    <mt-swipe :auto="4000">
      <mt-swipe-item v-for="item in topImages" :key='item.index'>
          <img :src="item">
      </mt-swipe-item>
    </mt-swipe>
  </div>
</template>

<script>
export default {
  props:{
    topImages:{
      type:Array,
      default() {
        return []
      }
    }
  }
}
</script>

<style scoped>
.swiper {
    height: 300px;
  }

  .swiper img {
    width: 100%;
  }
</style>