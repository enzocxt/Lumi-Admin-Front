<template>
  <el-form class="login-container" 
    label-position="left" 
    label-width="0px"
    v-loading="loading"
  >
    <h3 class="login-title">系统登录</h3>
    <el-form-item prop="username">
      <el-input type="text" v-model="loginForm.username"
        auto-complete="off" placeholder="账号"
      ></el-input>
    </el-form-item>
    <el-form-item prop="password">
      <el-input type="password" v-model="loginForm.password"
        auto-complete="off" placeholder="密码"
      ></el-input>
    </el-form-item>
    <el-checkbox class="login_remember" v-model="checked"
      label-position="left"
    >
      <span style="color: #505458">记住密码</span>
    </el-checkbox>
    <el-form-item style="width: 100%">
      <el-button type="primary" style="width: 40%;background:#505458;border:none"
        v-on:click="login"
      >登录</el-button>
      <router-link to="register">
        <el-button type="primary" style="width: 40%;background: #505458;border: none">注册</el-button>
      </router-link>
    </el-form-item>
  </el-form>
</template>

<script>

export default {
  name: 'Login',
  data () {
    return {
      rules: {
        username: [{required: true, message: '用户名不能为空', trigger: 'blur'}],
        password: [{required: true, message: '密码不能为空', trigger: 'blur'}]
      },
      checked: true,
      loginForm: {
        username: '',
        password: ''
      },
      loading: false,
    }
  },
  methods: {
    login () {
      var _this = this
      _this.$axios
        .post('/login', {
          username: this.loginForm.username,
          password: this.loginForm.password
        })
        .then(resp => {
          console.log("login response:\n", resp)
          if (resp.status === 200) {
            let data = resp.data
            console.log("response data:\n", data)
            _this.$store.commit('login', data)
            let path = _this.$route.query.redirect
            const newPath = path === '/' || path === undefined ? '/index' : path
            console.log("redirect path:\n", newPath)
            _this.$router.replace({
              path: newPath
            })
          } else {
            this.$alert(resp.message, '提示', {
              confirmButtonText: '确定'
            })
          }
          // if (resp.data.code === 200) {
          //   var data = resp.data.result
          //   // console.log("response data:\n", data)
          //   _this.$store.commit('login', data)
          //   var path = _this.$route.query.redirect
          //   const newPath = path === '/' || path === undefined ? '/index' : path
          //   // console.log("redirect path:\n", newPath)
          //   _this.$router.replace({
          //     path: newPath
          //   })
          // } else {
          //   this.$alert(resp.data.message, '提示', {
          //     confirmButtonText: '确定'
          //   })
          // }
        })
        .catch(failResponse => {})
    }
  }
}
</script>

<style>
.login-container {
  border-radius: 15px;
  background-clip: padding-box;
  margin: 90px auto;
  width: 350px;
  padding: 35px 35px 15px 35px;
  background: #fff;
  border: 1px solid #eaeaea;
  box-shadow: 0 0 25px #cac6c6;
}

.login-title {
  margin: 0px auto 40px auto;
  text-align: center;
  color: #505458;
}

.login_remember {
  margin: 0px 0px 35px 0px;
  text-align: left;
}
</style>
