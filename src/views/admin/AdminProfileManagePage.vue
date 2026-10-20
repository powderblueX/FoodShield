<script setup>
import {onMounted, reactive} from "vue";
import {getWithToken, removeToken} from "@/net/index.js";
import {ElMessage} from "element-plus";
import router from "@/router/index.js";

function logoutSuccess(data) {
  removeToken()
  ElMessage.success('退出登录成功')
  router.push("/")
}

function userLogout() {
  getWithToken('/api/auth/logout', logoutSuccess)
}

function getPersonalInfo() {
  getWithToken('/api/account/person-info', (data) => {
    form.username = data.username
    form.email = data.email
  })
}

onMounted(() => {
  getPersonalInfo()
})

let form = reactive({
  username: '',
  email: ''
})
</script>

<template>
  <el-container style="height: 100%; width: 100%">
    <el-header style="display: flex; justify-content: space-between; align-items: center;">
      <h3>管理员个人中心</h3>        
    </el-header>
    
    <div class="container">
      <div class="card">
        <div class="item">
          <span class="label">用户名：{{ form.username }}</span>
        </div>

        <div class="item">
          <span class="label">邮箱：{{ form.email }}</span>
        </div>

        <div class="item">
          <el-button type="danger" @click="userLogout" plain class="logout-btn">退出登录</el-button>
        </div>
      </div>
    </div>
  </el-container>
</template>

<style scoped>
.el-header {
  background-color: #f5f5f5;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 18px;
  font-weight: bold;
  padding: 0 20px;
}

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  position: relative;
}

.container::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: url('/src/assets/images/AdminWelcome.jpg');
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  opacity: 0.37;
  z-index: 0;
}

.card {
  width: 100%;
  max-width: 400px;
  background-color: white;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  padding: 30px;
  text-align: left;
  z-index: 1;
}

.item {
  margin-bottom: 20px;
  font-size: 16px;
  color: #555;
}

.label {
  font-weight: bolder;
  font-size: x-large;
  color: #333;
}

.logout-btn {
  width: 100%;
  padding: 12px;
  font-size: 16px;
  border-radius: 5px;
  border: none;
  cursor: pointer;
  background-color: #ff4d4f;
  color: white;
  margin-top: 30px;
}

.logout-btn:hover {
  background-color: #f5222d;
}
</style>