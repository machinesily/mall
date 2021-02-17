<template>
  <div class="recommend">
    <div v-for="item in recommends" :key="item.index" class="recommend-item">
      <a :href="item.link"><img :src="item.image" alt=""></a>
      <div>{{item.title}}</div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      recommends: {
        type: Array,
        default: []
      }
    }
  }
</script>

<style>
  .recommend {
    display: flex;
    text-align: center;
    font-size: 16px;
    padding: 10px 0 20px;
    border-bottom: 5px solid #eeeeee;
  }

  .recommend-item {
    flex: 1;
  }

  .recommend-item img {
    width: 80%;
    margin-bottom: 5px;
  }
</style>