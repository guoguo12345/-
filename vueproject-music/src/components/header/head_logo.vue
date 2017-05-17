<template>
  <div class="logo-container">
    <div class="head-download">
      <router-link to="/index">爱音乐</router-link>
      <router-link to="/login">登录</router-link>
    </div>
    <div class="head-search" @click="searchRouter">
      <img src="http://m.kugou.com/v3/static/images/index/search.png">
    </div>
  </div>
</template>

<script type="es6">
  export default {
    name: 'head-logo',
    methods: {
      searchRouter(){
        this.$store.commit('showDetailPlayer',false);
        this.$router.push({path: '/search'});
      }
    }
  }
</script>
