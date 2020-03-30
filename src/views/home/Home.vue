<template>
  <div id="home">
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
    <van-swipe class="my-swipe" :autoplay="3000" indicator-color="white">
      <van-swipe-item v-for="(image, index) in banners" :key="index">
        <img :src="image.image" alt="">
      </van-swipe-item>
    </van-swipe>
    <recommend-view :recommends='recommends'></recommend-view>
  </div>
</template>

<script>
  import NavBar from '../../components/common/navbar/NavBar'
  import {getHomeMultiData} from '../../network/home'
  import RecommendView from './childComps/RecommendView'

  export default {
    name: "Home",
    components:{
      NavBar,
      RecommendView
    },
    data(){
      return{
        banners:[],
        recommends:[]
      }
    },
    created() {
      getHomeMultiData().then(res => {
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
        console.log(res.data);
      })
    }
  }
</script>

<style scoped>
  .home-nav{
    background: var(--color-tint);
    color: #ffffff;
  }

  .my-swipe .van-swipe-item img{
    width: 100%;
  }
</style>
