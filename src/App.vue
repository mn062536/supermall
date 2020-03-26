<template>
  <div id="app">
    <router-view></router-view>
    <main-tar-bar></main-tar-bar>
  </div>
</template>

<script>
  import MainTarBar from 'components/content/maintarbar/MainTarBar'
  export default {
    name: 'app',
    components: {
      MainTarBar
    }
  }
</script>

<style>
  /*css 引入方式*/
  @import "assets/css/base.css";
</style>
