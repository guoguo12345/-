<template>
  <div class="logo-container">
    <div class="head-download">
      <router-link to="/index">爱音乐</router-link>
      <router-link to="/login" class="login">登录</router-link>
      <router-link to="/register" class="register">注册</router-link>
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
    },
    mounted() {
      var phone = localStorage.getItem('phone');
      if(phone){
        $('header .login').html('注销');
        $('header .register').html('欢迎您,'+phone);
        $('header .register').attr('href','/#/index');
        $('header .login').tap(function(){
          localStorage.removeItem('phone');
          $('header .register').html('注册');
          $('header .login').html('登录');
          $('header .register').attr('href','/#/register');
        });
      }
    }
  }
</script>
