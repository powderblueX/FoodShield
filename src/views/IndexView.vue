<script setup>
import {ref} from "vue";
import router from "@/router/index.js";
import {
  House,
  List,
  ChatLineSquare,
  Document,
  PieChart,
  MessageBox,
  Notebook,
  UserFilled
} from '@element-plus/icons-vue';

const faviconSrc = ref(new URL('/src/assets/images/foodSafety.ico', import.meta.url).href);

let activeMenu = ref('/index')

function handleSelect(index){
  router.push(index)
  activeMenu = index
}
</script>



<template>
  <div class="container">
    <div class="navigation">
      <el-menu :default-active="activeMenu" @select="handleSelect" mode="horizontal" router>
        <el-header>
          <el-image style="width: 60px; height: 60px;" :src="faviconSrc" fit="cover" alt="图片加载失败"
                    @load="handleImageLoad" @error="handleImageError">
            <template #placeholder>
              <div style="color: #999;">加载中...</div>
            </template>
          </el-image>
          <h1 style="font-size: x-large; font-family: KaiTi;">校园食品安全管理平台</h1>
        </el-header>
        <el-menu-item index="/index"><el-icon><House/></el-icon>首页</el-menu-item>
        <el-menu-item index="/index/post"><el-icon><ChatLineSquare/></el-icon>留言板</el-menu-item>
        <el-menu-item index="/index/trace"><el-icon><List/></el-icon>食品溯源</el-menu-item>
        <el-menu-item index="/index/report"><el-icon><PieChart/></el-icon>食品报告</el-menu-item>
        <el-menu-item index="/index/complaint"><el-icon><MessageBox/></el-icon>投诉</el-menu-item>
        <el-menu-item index="/index/account"><el-icon><UserFilled/></el-icon>我的</el-menu-item>
      </el-menu>
    </div>

    <div class="content">
      <router-view style="margin-top: 20px"></router-view>
    </div>
  </div>
</template>



<style scoped>
.container {
  display: flex;
  flex-direction: column;
  height: 100%;
}

.navigation {
  flex: 1;
  width: 100%;
}

.el-header {
  display: flex;
  align-items: center;
}

.el-menu{
  display: flex; 
  justify-content: space-evenly
}

.content {
  flex: 14;
  width: 100%;
}
</style>