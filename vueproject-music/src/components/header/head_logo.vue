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
    data(){
      return {
        isReload: false
      }
    },
    methods: {
      searchRouter(){
        this.$store.commit('showDetailPlayer',false);
        this.$router.push({path: '/search'});
      }
    },
    mounted() {
      var phone = localStorage.getItem('phone');
      var loginDom = document.getElementsByClassName("login")[0];
      var registerDom = document.getElementsByClassName("register")[0];
      if(phone) {
        var isReload = false;
        loginDom.innerHTML = '注销';
        registerDom.innerHTML = phone;
        registerDom.setAttribute('href','/#/index');
        console.log(this.isReload);
        if(!this.isReload) {
          // window.location.reload();
          this.isReload = true;
        }
        console.log(this.isReload);
        loginDom.onclick = function(){
          localStorage.removeItem('phone');
          registerDom.innerHTML = '注册';
          loginDom.innerHTML = '登录';
          registerDom.setAttribute('href','/#/register');
        };
      }
    }
  }
</script>
