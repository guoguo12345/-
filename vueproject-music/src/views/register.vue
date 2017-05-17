<template>
	<div id="registor">
		<h3>注册页面</h3>
		<form class="form-horizontal">
          <div class="form-group">
            <label for="inputEmail3" class="col-sm-2 control-label">账号</label>
            <div class="col-sm-10">
              <input type="text" class="form-control phone" id="inputEmail3" placeholder="仅支持大陆手机号码" required>
            </div>
          </div>
          <div class="form-group">
            <label for="inputPassword3" class="col-sm-2 control-label">密码</label>
            <div class="col-sm-10">
              <input type="password" class="form-control password" id="inputPassword3" placeholder="输入密码,不少于6位数字或字母" required>
            </div>
          </div>
          <div class="form-group">
            <label for="inputPassword3" class="col-sm-2 control-label">确认密码</label>
            <div class="col-sm-10">
              <input type="password" class="form-control" id="inputPassword3" placeholder="输入密码,不少于6位数字或字母" required>
            </div>
          </div>
          <div class="form-group">
            <div class="col-sm-offset-2 col-sm-10">
            	<button type="submit" class="btn btn-info btn-lg" @click="registor">注  册</button>
              <router-link to="/login" class="btn btn-success btn-lg">登录</router-link>
            </div>
          </div>
        </form>
	</div>
</template>
<script>
	import { PLAY_AUDIO } from '../mixins'
	export default {
	    mixins: [PLAY_AUDIO],
	    data(){
	      return {
	        opacity: 0,
	        data: ""
	      }
	    },
	    methods: {
	    	registor() {
				var phone = document.getElementsByClassName("phone")[0].value;
		        var password = document.getElementsByClassName("password")[0].value;
		        console.log(phone);
		        console.log(password);
		        this.$http.post("/users/register",{
		              "phone": phone,
		              "password": password
		        }).then(function(data) {
		            this.data = data.data;
		            if(this.data=='用户名不存在'){
						localStorage.setItem('phone',phone);
						location.href = '/#/index';
					}
		        },function(){
		              console.log(err);
		        });
			}
	    },
	    //通过路由的before钩子解除router-view缓存限制
	    beforeRouteEnter (to, from, next) {
	      next(vm => {
	        vm.$store.commit('showHead', true);
	        vm.get();
	        window.onscroll = ()=> {
	          vm.opacity = window.pageYOffset / 250;
	          vm.$store.commit('setHeadStyle', {background: `rgba(43,162,251,${vm.opacity})`});
	        }
	      })
	    },
	    beforeRouteLeave(to, from, next){
	      this.$store.commit('showHead', false);
	      window.onscroll = null;
	      next();
	    }
	}
</script>
<style scoped>
	h3 {padding-bottom: 20px;color: #2CA2F9;}
	#registor {
    	padding: 0 35px;
	} 
</style>
 

