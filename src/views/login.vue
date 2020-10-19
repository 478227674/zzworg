<template>
  <div>
<!--    <el-form ref="loginForm" :model="form" :rules="rules" label-width="80px" class="login-box">-->
<!--      <h3 class="login-title">欢迎登录</h3>-->
<!--      <el-form-item label="账号" prop="userName">-->
<!--        <el-input type="text" placeholder="请输入账号" v-model="form.userName"/>-->
<!--      </el-form-item>-->
<!--      <el-form-item label="密码" prop="passWord">-->
<!--        <el-input type="password" placeholder="请输入密码" v-model="form.passWord"/>-->
<!--      </el-form-item>-->
<!--      <el-form-item>-->
<!--        <el-button type="primary" v-on:click="onSubmit('loginForm')">登录</el-button>-->
<!--      </el-form-item>-->
<!--    </el-form>-->

<!--    <el-dialog-->
<!--      title="温馨提示"-->
<!--      :visible.sync="dialogVisible"-->
<!--      width="30%"-->
<!--      :before-close="handleClose">-->
<!--      <span>请输入账号和密码</span>-->
<!--      <span slot="footer" class="dialog-footer">-->
<!--        <el-button type="primary" @click="dialogVisible = false">确 定</el-button>-->
<!--      </span>-->
<!--    </el-dialog>-->
    <div class="login-box">
      <div class="pc-center">
        <div class="login-form">
          <div class="login-b">
            <div class="login-l">
              <img src="./loginperson.png" alt="">
            </div>
            <div class="login-r">
              <div class="login-title">元儒教育城产品管理后台</div>
              <ul class="login-form-item">
                <li>
                  <img src="./loginusername.png" alt="">
                  <input v-model="form.userName" placeholder="请输入手机号" type="text">
                </li>
                <li>
                  <img src="./loginpassword.png" alt="">
                  <input v-model="form.passWord" placeholder="请输入登录密码" type="password">
                </li>
              </ul>
              <div class="login-btn" @click="onSubmit">登录</div>
<!--              <div class="commpany">Copyright@1998-2014 太奇教育 .All Rights Reserved</div>-->
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import { mapActions } from "vuex";

  export default {
    name: "Login",
    data() {
      return {
        form: {
          userName: '',
          passWord: ''
        },

        // 表单验证，需要在 el-form-item 元素中增加 prop 属性
        rules: {
          username: [
            {required: true, message: '账号不可为空', trigger: 'blur'}
          ],
          password: [
            {required: true, message: '密码不可为空', trigger: 'blur'}
          ]
        },

        // 对话框显示和隐藏
        dialogVisible: false
      }
    },
    methods: {
      ...mapActions(['setUser']),
      handleClose:function () {

      },
      onSubmit:function(formName) {
        this.http.post('/orgLogin/login', this.form).then(res=>{
          console.log(res)
          if(res.code == 0){
            this.$message({
              message: '登陆成功',
            });
            this.setUser(res.data)
            localStorage.setItem('userinfo',JSON.stringify(res.data))
            this.$router.push("/home");
            location.reload();
          }
        })
      }
    }
  }
  import './login.css'

</script>

<style scoped>
  /*.login-box {*/
  /*  border: 1px solid #DCDFE6;*/
  /*  width: 350px;*/
  /*  margin: 180px auto;*/
  /*  padding: 35px 35px 15px 35px;*/
  /*  border-radius: 5px;*/
  /*  -webkit-border-radius: 5px;*/
  /*  -moz-border-radius: 5px;*/
  /*  box-shadow: 0 0 25px #909399;*/
  /*}*/

  /*.login-title {*/
  /*  text-align: center;*/
  /*  margin: 0 auto 40px auto;*/
  /*  color: #303133;*/
  /*}*/
</style>
