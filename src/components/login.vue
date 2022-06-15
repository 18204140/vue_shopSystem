<template>
  <div class="login_container">
    <div class='login_box'>
      <!-- 表单区域 -->
      <el-form ref="formRef" class="form" :model="form" :rules="rules">
        <!-- 用户名 -->
        <el-form-item prop="username">
          <el-input  prefix-icon="iconfont icon-yonghu" v-model="form.username"></el-input>
        </el-form-item>
        <!-- 密码 -->
        <el-form-item prop="password">
          <el-input prefix-icon="iconfont icon-mima" v-model="form.password" show-password></el-input>
        </el-form-item>
        <el-form-item class="btns">
          <el-button type="primary" @click='login'>登录</el-button>
          <el-button type="info" @click="reset">重置</el-button>
        </el-form-item>
      </el-form>

    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      form: {
        username: 'zs',
        password: '123456'
      },
      rules: {
        // 验证用户名是否合法
        username: [
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min: 1, max: 10, message: '长度在 1 到 10 个字符', trigger: 'blur' }
        ],
        // 验证密码是否合法
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 6, max: 15, message: '长度在 6 到 15 个字符', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    reset () {
      this.$refs.formRef.resetFields()
    },
    login () {
      this.$refs.formRef.validate((val) => {
        if (!val) return
        // 发请求
        // const {data:res} = this.$http.post('login', this.form)
        this.$message.success('登录成功')
        // 将登录成功之后的token,保存到客户端sessionStorage中
        // 1.1项目中除了登录之外的接口，必须在登录之后才能访问
        // window.sessionStorage.setItem('token',res.data.token)
        this.$router.push('/home')
      })
    }
  }

}
</script>

<style lang="less" scoped>
.login_container {
  width: 100%;
  height: 100%;
  background: #2b4b6b;
}
.login_box {
  width: 450px;
  height: 300px;
  background: #fff;
  border-radius: 3px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%)
}
.btns {
  display: flex;
  justify-content:flex-end;
}
.form {
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: 0 20px;
  box-sizing: border-box;
}
</style>
