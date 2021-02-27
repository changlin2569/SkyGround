<template>
  <div class="container">
    <div class="login">
      <div class="avatar">
        <img src="../assets/logo.png" alt="" />
      </div>
      <div class="form">
        <el-form ref="loginFormRef" :rules="loginFormRules" :model="loginForm" label-width="100px">
          <el-form-item label="用户名：" prop="name">
            <el-input v-model="loginForm.name"></el-input>
          </el-form-item>
          <el-form-item label="密码：" prop="password">
            <el-input v-model="loginForm.password" type="password"></el-input>
          </el-form-item>
        </el-form>
      </div>
      <div class="button_container">
          <el-button type="primary">登录</el-button>
          <el-button type="info">注册</el-button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      loginForm: {
        name: 'admin',
        password: 123456
      },
      loginFormRules: {
        name: [
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min: 3, max: 6, message: '长度在 3 到 6 个字符', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 6, max: 12, message: '长度在 3 到 5 个字符', trigger: 'blur' }
        ]
      }
    }
  }
}
</script>

<style lang="less" scoped>
.container {
  position: relative;
  height: 100%;
  background-color: aquamarine;
  .login {
    position: absolute;
    width: 400px;
    height: 300px;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
  }
  .avatar {
    position: absolute;
    width: 100px;
    height: 100px;
    left: 50%;
    transform: translate(-50%, -50%);
    border: 1px solid green;
    border-radius: 50%;
    overflow: hidden;
    background-color: #fff;
    img {
      width: 100%;
      height: 100%;
    }
  }
  .form {
      position: absolute;
      height: 100px;
      top: 70px;
  }
  .el-form {
      width: 350px;
  }
  .button_container {
      position: absolute;
      bottom: 50px;
      right: 50px;
  }
}
</style>
