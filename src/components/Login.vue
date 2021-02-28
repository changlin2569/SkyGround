<template>
  <div class="container">
    <div class="login">
      <div class="avatar">
        <img src="../assets/logo.png" alt="" />
      </div>
      <div class="form">
        <el-form
          ref="loginFormRef"
          :rules="loginFormRules"
          :model="loginForm"
          label-width="100px"
        >
          <el-form-item label="手机号：" prop="phone">
            <el-input v-model="loginForm.phone"></el-input>
          </el-form-item>
          <el-form-item label="验证码：" prop="noteCode">
            <el-input v-model="loginForm.noteCode">
              <el-button slot="append" :disabled="noteCodeBtn"
              @click="getNoteCode"
                >{{noteCodeValue}}</el-button
              >
            </el-input>
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
        phone: '',
        noteCode: ''
      },
      loginFormRules: {
        phone: [
          { required: true, message: '请输入手机号', trigger: 'blur' }
        ],
        noteCode: [
          { required: true, message: '请输入验证码', trigger: 'blur' }
        ]
      },
      // 控制发送验证码按钮的禁用
      noteCodeBtn: false,
      // 验证码按钮文本
      noteCodeValue: '获取验证码',
      wait: 60
    }
  },
  methods: {
    getNoteCode () {
      const reg = /^1[3|4|5|7|8][0-9]{9}$/
      if (!reg.test(this.loginForm.phone)) {
        this.$message.error('请输入正确的手机号码')
        return false
      }
      this.noteCodeBtn = true
      this.getNoteCodeHandle()
      this.$message.success('验证码已发送')
    },
    getNoteCodeHandle () {
      if (this.wait > 0) {
        this.wait--
        this.noteCodeValue = `重新获取${this.wait}`
        setTimeout(() => {
          this.getNoteCodeHandle()
        }, 1000)
      } else {
        this.noteCodeBtn = false
        this.noteCodeValue = '获取验证码'
        this.wait = 60
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
