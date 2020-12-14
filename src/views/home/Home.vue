<template>
  <div id="home">
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
  </div>
</template>

<script>
  import NavBar from 'components/common/navbar/NavBar.vue'
  import {getHomeMultidata} from 'network/home'

  export default {
    components: {
      NavBar,
    },
    data () {
      return {
      banners:[],
      recommends:[]  
      }
    },
    created(){
      getHomeMultidata().then(res =>{
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
  
</style>