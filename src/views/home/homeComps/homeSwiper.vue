<template>
  <div class="swiper">
    <mt-swipe :auto="4000">
      <mt-swipe-item v-for="item in banners" :key='item.index'>
        <a :href="item.link">
          <img :src="item.image" alt="">
        </a>
      </mt-swipe-item>
    </mt-swipe>
  </div>
</template>

<script>
  export default {
    props: {
      banners: {
        type: Array,
        default () {
          return []
        }
      }
    }
  }
</script>

<style>
  .swiper {
    height: 150px;
  }

  .swiper img {
    width: 100%;
  }
</style>