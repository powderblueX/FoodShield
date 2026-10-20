<script setup>
import { ref } from "vue";
const FoodSafetyArctleSrc = ref(new URL('/src/assets/images/FoodSafetyArticle.jpg', import.meta.url).href);
const FoodInfoSrc = ref(new URL('/src/assets/images/FoodInfo.jpg', import.meta.url).href);
const ReportSrc = ref(new URL('/src/assets/images/Report.jpg', import.meta.url).href);
const PostAndComplaintSrc = ref(new URL('/src/assets/images/PostAndComplaint.jpg', import.meta.url).href);
</script>

<template>
  <div class="container">
    <div class="left">
      <el-card>
        <el-image :src="FoodSafetyArctleSrc" alt="食品安全文章"></el-image>
      </el-card>
      <el-card>
        <el-image :src="FoodInfoSrc" alt="食品信息"></el-image>
      </el-card>
    </div>
    <div class="center">
      <h1 style="font-size: xx-large; font-family: KaiTi;">校园食品安全管理平台</h1>
      <el-card>
        <router-view v-slot="{ Component }">
          <transition name="el-fade-in-linear" mode="out-in">
            <component :is="Component"/>
          </transition>
        </router-view>
      </el-card>
    </div>
    <div class="right">
      <el-card>
        <el-image :src="ReportSrc" alt="食品安全数据报告"></el-image>
      </el-card>
      <el-card>
        <el-image :src="PostAndComplaintSrc" alt="食品安全留言板与投诉"></el-image>
      </el-card>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  height: 100vh;
  background-image: url('/src/assets/images/background.jpg');
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
}

.left, .center, .right {
  padding: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.left {
  flex: 2;
}

.center {
  flex: 1;
}

.right {
  flex: 2;
}

.left .el-card,
.right .el-card {
  margin: 50px; 
  width: 370px;
  height: 370px;
  opacity: 0; /* 初始状态为透明 */
}

.el-header {
  font-family: KaiTi;
  font-size: xx-large;
  font-weight: bolder;
}

@keyframes fadeInFromLeft {
  from {
    opacity: 0;
    transform: translateX(-50%);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes fadeInFromRight {
  from {
    opacity: 0;
    transform: translateX(50%);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.left .el-card {
  animation: fadeInFromLeft 1s ease forwards; 
}

.right .el-card {
  animation: fadeInFromRight 1s ease forwards;
}

.left .el-card:nth-child(1),
.right .el-card:nth-child(1) {
  animation-delay: 0.3s;
}

.left .el-card:nth-child(2),
.right .el-card:nth-child(2) {
  animation-delay: 0.6s;
}
</style>
