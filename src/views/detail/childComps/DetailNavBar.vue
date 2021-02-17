<template>
  <div>
    <nav-bar>
      <div slot="left" class="left" @click="back">
        <img src="~assets/img/common/back.svg">
      </div>
      <div slot="center" class="title">
        <div class="title-item" :class="{active: index === currentIndex}" v-for="(item,index) in titles" :key="index" @click="itemClick(index)">{{item}}</div>
      </div>
    </nav-bar>
  </div>
</template>

<script>
  import NavBar from 'components/common/navbar/NavBar.vue'
  export default {
    components: {
      NavBar
    },
    data() {
      return {
        titles: ['商品', '参数', '评论', '推荐'],
        currentIndex: 0
      }
    },
    methods:{
      itemClick(index){
        this.currentIndex = index;
      },
      back(){
        this.$router.back()
      }
    },  
  }
</script>

<style>
  .left{
    margin-top: 4px;
  }
  .title {
    display: flex;
    font-size: 13px;
  }

  .title-item {
    flex: 1;
  }

  .active{
    color: var(--color-high-text);
  }
</style>