<script>
import request from "@/utils/request";
export default {
  name: "Register",
  data(){
    return {
      form:{},
      loading: false
    }
  },
  methods:{
    register(){
      if(this.form.password !== this.form.conforms){
        this.$message({
          type: 'error',
          message: '两次密码不一致'
        });
        return;
      }
      this.loading = true;
      request.post("/user/register",this.form).then(res=>{
        if(res.code === '0'){
          this.$message({
            type: 'success',
            message: '注册成功'
          })
          this.$router.push('/login')
        }else{
          this.$message({
            type: 'error',
            message: res.msg
          });
        }
      }).finally(() => {
        this.loading = false;
      })
    },
    goToLogin() {
      this.$router.push('/login')
    }
  }
}
</script>

<template>
  <div class="register-container">
    <div class="register-box">
      <div class="register-title">
        <h2>欢迎注册</h2>
        <p>Create Account</p>
      </div>
      <el-form ref="form" :model="form" size="large" class="register-form">
        <el-form-item prop="username">
          <el-input
              v-model="form.username"
              placeholder="请输入用户名"
          >
            <template #prefix>
              <el-icon><User /></el-icon>
            </template>
          </el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input
              v-model="form.password"
              show-password
              placeholder="请输入密码"
          >
            <template #prefix>
              <el-icon><Lock /></el-icon>
            </template>
          </el-input>
        </el-form-item>
        <el-form-item prop="conforms">
          <el-input
              v-model="form.conforms"
              show-password
              placeholder="请再次确认密码"
          >
            <template #prefix>
              <el-icon><Lock /></el-icon>
            </template>
          </el-input>
        </el-form-item>
        <el-form-item>
          <el-button
              type="primary"
              class="register-button"
              :loading="loading"
              @click="register"
          >
            注册
          </el-button>
        </el-form-item>
        <div class="login-link">
          已有账号？<span @click="goToLogin">立即登录</span>
        </div>
      </el-form>
    </div>
  </div>
</template>

<style scoped>
.register-container {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: linear-gradient(135deg, #91cd9d 0%, #639e4e 100%);
  overflow: hidden;
}

.register-box {
  width: 420px;
  padding: 40px;
  background: rgba(255, 255, 255, 0.95);
  border-radius: 16px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(10px);
  animation: fadeIn 0.5s ease;
}

.register-title {
  text-align: center;
  margin-bottom: 40px;
}

.register-title h2 {
  color: #333;
  font-size: 28px;
  margin-bottom: 8px;
}

.register-title p {
  color: #666;
  font-size: 16px;
}

.register-form {
  margin-top: 20px;
}

.register-button {
  width: 100%;
  height: 44px;
  font-size: 16px;
  border-radius: 22px;
  background: linear-gradient(135deg, #667eea 0%, #66ac56 100%);
  border: none;
  transition: all 0.3s ease;
}

.register-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.login-link {
  text-align: center;
  margin-top: 20px;
  color: #666;
}

.login-link span {
  color: #667eea;
  cursor: pointer;
  font-weight: 500;
  transition: color 0.3s ease;
}

.login-link span:hover {
  color: #764ba2;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

:deep(.el-input__wrapper) {
  border-radius: 22px;
  padding: 8px 15px;
}

:deep(.el-input__inner) {
  height: 44px;
  line-height: 44px;
}
</style>