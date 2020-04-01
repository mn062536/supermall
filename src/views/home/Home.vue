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
    <feature-view></feature-view>
    <tab-control class="tab-control" :ctitles="['流行', '新款', '精选']" @tabClick="pTabClick" />
    <goods-list :goods="goods[currentType].list"></goods-list>
  </div>
</template>

<script>
  import NavBar from '../../components/common/navbar/NavBar'
  import TabControl from '../../components/content/tabControl/TabControl'
  import GoodsList from '../../components/content/goods/GoodsList'

  import RecommendView from './childComps/RecommendView'
  import FeatureView from './childComps/FeatureView'

  import { getHomeMultiData, getHomeGoods } from '../../network/home'

  export default {
    name: "Home",
    components:{
      NavBar,
      TabControl,
      GoodsList,
      RecommendView,
      FeatureView
    },
    data(){
      return{
        banners:[],
        recommends:[],
        goods:{
          'pop':{page:0,list:[]},
          'new':{page:0,list:[]},
          'sell':{page:0,list:[]},
        },
        currentType:'pop'
      }
    },
    created() {
      // 1.请求数据
      this.getHomeMultiData();
      // 2.请求商品数据
      this.getHomeGoods('pop');
      this.getHomeGoods('new');
      this.getHomeGoods('sell');
    },
    methods:{

      //事件监听相关方法
      pTabClick(index){
        switch (index) {
          case 0:
            this.currentType = 'pop'
            break
          case 1:
            this.currentType = 'new'
            break
          case 2:
            this.currentType = 'sell'
        }
      },

      //网络请求相关
      getHomeMultiData(){
        getHomeMultiData().then(res => {
          this.banners = res.data.banner.list;
          this.recommends = res.data.recommend.list;
          //console.log(res.data);
        })
      },

      // 2.请求商品数据
      getHomeGoods(type){
        const page = this.goods[type].page + 1
        getHomeGoods(type,page).then(res => {
          //console.log(res.data.list);
          this.goods[type].list.push(...res.data.list)
          this.goods[type].page += 1
        })
      }
    }
  }
</script>

<style scoped>
  #home{
    padding-top: 44px;
  }
  .home-nav{
    background: var(--color-tint);
    color: #ffffff;
    position: fixed;
    top: 0;
    right: 0;
    left: 0;
    z-index: 999;
  }

  .my-swipe .van-swipe-item img{
    width: 100%;
  }

  .tab-control{
    position: sticky;
    top: 44px;
    z-index: 99999;
  }
</style>
