<template>
    <div class="login_container">
<!--      头像区-->
      <div class="login_box">
        <div class="avater_box">
          <img src="../assets/logo.png" alt="">
        </div>
        <!--        登录表单区-->
        <el-form ref="loginFormRef" :model="loginForm"
                 :rules="loginFormRules" label-width="0px" class="login_form">
<!--          用户名-->
          <el-form-item prop="username">
            <el-input v-model="loginForm.username" prefix-icon="iconfont icontouxiang" >

            </el-input>
          </el-form-item>

<!--        密码区-->

          <el-form-item prop="password">
            <el-input v-model="loginForm.password" prefix-icon="iconfont iconlock"
            type="password">

            </el-input>
          </el-form-item>

<!--        按钮区-->

          <el-form-item class="bnts">
            <el-button type="primary" @click="login">登录</el-button>
            <el-button type="info" @click="resetLoginForm">重置</el-button>
          </el-form-item>
        </el-form>
      </div>
    </div>
</template>

<script>
export default {
  data() {
    return{
      // 这是等率表单的对象
      loginForm:{
        username: "zd",
        password: "123"
      },
      loginFormRules:{
        username:[{ required: true, message: '请输入登录名', trigger: 'blur' },
          { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }],
        password:[{ required: true, message: '请输入密码', trigger: 'blur' },
          { min: 6, max: 15, message: '长度在 6 到 15个字符', trigger: 'blur' }]
      }
    }
  },
  methods:{
    resetLoginForm(){
      // console.log(this)
      this.$refs.loginFormRef.resetFields();
    },
    login(){
      this.$refs.loginFormRef.validate(function (valid,obj) {
        if(!valid) return;
        const result=this.$http.post('login', this.loginForm);
      })
    }
  }
  // watch:{
  //   "loginForm.username"(hj, yu){
  //     console.log('new: %s, old: %s', hj, yu)
  //   }
  // }
}
</script>

<style lang="less" scoped>
.login_container{
  background-color: #2b4b6b;
  height: 100%;
}
.login_box{
  width: 450px;
  height: 300px;
  background-color: #fff;
  border-radius: 3px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
.avater_box{
  height: 130px;
  width: 130px;
  border: 1px solid #eee;
  border-radius: 50%;
  padding: 10px;
  box-shadow: 0 0 10px #ddd;
  position: absolute;
  left: 50%;
  transform: translate(-50%,-50%);
  background-color: #ffffff;
  img{
    width: 100%;
    height: 100%;
    border-radius: 50%;
    background-color: #eee;
  }
}
.bnts{
  display: flex;
  justify-content: flex-end;
}
.login_form{
  position: absolute;
  bottom: 0;
  /*lafe: 0;*/
  width: 100%;
  padding: 0 20px;
  box-sizing: border-box;

}


</style>
