<template>
  <div class="log_top">
    <div class="log_content">
      <h1>后台管理系统</h1>
      <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
        <el-form-item label="用户名" prop="username">
          <el-input v-model="ruleForm.username" placeholder="请输入用户名"></el-input>
        </el-form-item>
        <el-form-item label="密码" prop="password">
          <el-input v-model="ruleForm.password" placeholder="请输入密码"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="submitForm('ruleForm')">登录</el-button>
          <el-button @click="resetForm('ruleForm')">重置</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
import LoginApi from './http/api.js'
export default {
  data() {
    return {
      ruleForm: {
        username: 'admin',
        password: '123456'
      },
      rules: {
        username: [
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min: 3, max: 20, message: '长度在 3 到 20 个字符', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 3, max: 20, message: '长度在 3 到 20 个字符', trigger: 'blur' }
        ],
      }
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate(async (valid) => {
        if (valid) {
          const res = await LoginApi(this.ruleForm)
          console.log('返回的状态码：', res);
          this.$router.push('/home')
        } else {
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    }
  }
}
</script>

<style scoped>
.log_top {
  width: 100%;
  height: 100%;
  position: relative;
  margin: 0 auto;
}

.log_content {
  width: 600px;
  height: 300px;
  line-height: 60px;
  padding: 0 30px;
  position: absolute;
  top: 25%;
  left: 50%;
  margin-left: 0px;
  transform: translate(-50%, 0%);
  text-align: center;
  background-color: white;
  box-shadow: 0 0 4px 4px yellow;
}
</style>
