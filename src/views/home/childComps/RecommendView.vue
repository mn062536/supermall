<template>
  <div class="recommend">
    <div v-for="item in recommends" class="recommend-item">
      <a :href="item.link">
        <img :src="item.image" alt />
        <div>{{item.title}}</div>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: "RecommendView",
  props: {
    recommends: {
      type: Array,
      default() {
        return [];
      }
    }
  }
};
</script>

<style scoped>
  .recommend{
    display: flex;
    justify-content: space-around;
    margin: 15px 0;
    padding-bottom: 10px;
    border-bottom: 10px #eeeeee solid;
    font-size: 14px;
    text-align: center;
  }
  .recommend-item div{
    padding-top: 5px;
  }
  
  .recommend-item img{
    width: 65px;
  }
</style>
