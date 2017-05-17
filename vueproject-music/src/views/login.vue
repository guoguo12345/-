 <template>
	<div id="login">
    <h3>登录页面</h3>
		<form class="form-horizontal">
          <div class="form-group">
            <label for="inputEmail3" class="col-sm-2 control-label">手机号码</label>
            <div class="col-sm-10">
              <input type="text" class="form-control phone" id="inputEmail3" placeholder="手机号码" required>
            </div>
          </div>
          <div class="form-group">
            <label for="inputPassword3" class="col-sm-2 control-label">密码</label>
            <div class="col-sm-10">
              <input type="password" @blur="loginFunc" class="form-control password" id="inputPassword3" placeholder="输入密码" required>
            </div>
          </div>
          <div class="form-group">
            <div class="col-sm-offset-2 col-sm-10">
              <button type="button" class="btn btn-info btn-primary btn-lg" @click="save">登  录</button>
              <router-link to="/register" class="btn btn-success btn-lg">注册</router-link>
            </div>
          </div>
        </form>
	</div>
</template>
<script type="es6">
  import { PLAY_AUDIO } from '../mixins'
  export default {
    mixins: [PLAY_AUDIO],
    data(){
      return {
        opacity: 0,
        data: "",
      }
    },
    methods: {
        loginFunc() {
            var phone = document.getElementsByClassName("phone")[0].value;
            var password = document.getElementsByClassName("password")[0].value;
            this.$http.post("/users/login",{
                "phone": phone,
                "password": password
            }).then(function(data) {
                this.data = data.data;
                console.log(this.data);
            },function(){
                console.log(err);
            });
        },
        save(){
          var phone = document.getElementsByClassName("phone")[0].value;
          var password = document.getElementsByClassName("password")[0].value;
          this.$http.post("/users/login",{
              "phone": phone,
              "password": password
          }).then(function(data) {
                this.data = data.data;
                console.log(this.data);
                if(this.data=='密码正确'){
                  localStorage.setItem('phone',phone);
                  location.href = '/#/index';
                }else if(this.data=='密码错误') {
                    alert("密码错误");
                }else if(this.data=='用户名不存在') {
                    alert("用户名不存在");
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
    #login {
        padding: 0 35px;
    } 
</style>

