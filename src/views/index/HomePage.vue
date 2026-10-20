<script setup>
import { ref } from 'vue';
import {onMounted, reactive} from "vue";
import {get} from "@/net/index.js";
import router from "@/router/index.js";

const HomeImageSrc = ref(new URL('/src/assets/images/HomeImage.jpg', import.meta.url).href);

function getTopNews() {
  get('/api/news/top-news', (data) => {
    for (const item of data) {
      form.news.push({
        id: item.id,
        title: item.title,
        content: item.content,
        photo_url: item.photo_url,
        date: (new Date(item.date)).toLocaleString(),
      });
    }
  });
}

function getTopKnowledge() {
  get('/api/knowledge/top-knowledge', (data) => {
    for (const item of data) {
      form.knowledge.push({
        id: item.id,
        title: item.title,
        content: item.content,
        category: item.category,
        photo_url: item.photo_url,
        date: (new Date(item.date)).toLocaleString(),
      });
    }
  });
}

function getAllNews(){
  router.push('/all-news')
}

function getAllKnowledge(){
  router.push('/all-knowledge')
}

// 页面首次加载时运行
onMounted(() => {
  getTopNews();
  getTopKnowledge();
});

function showNewsDetail(newsItem) {
  router.push({
    name: 'news',
    params: {
      id: newsItem.id,
      title: newsItem.title,
      content: newsItem.content,
      photo_url: JSON.stringify(newsItem.photo_url),
      date: newsItem.date,
    },
  });
}

function showKnowledgeDetail(knowledgeItem) {
  router.push({
    name: 'knowledge',
    params: {
      id: knowledgeItem.id,
      category: knowledgeItem.category,
      title: knowledgeItem.title,
      content: knowledgeItem.content,
      photo_url: JSON.stringify(knowledgeItem.photo_url),
      date: knowledgeItem.date,
    },
  });
}

let form = reactive({
  news: [],
  knowledge: [],
});
</script>

<template>
  <div class="container">
    <div class="introduction">
      <el-container class="home">
      <el-image class="homeimage" :src="HomeImageSrc" fit="cover" alt="食品安全管理平台"></el-image>
      <div class="banner-content">
        <h1 style="font-size: xx-large; font-family: KaiTi;">食品安全管理平台</h1>
        <p>10年校园食品安全服务经验</p>
        <p>优质服务值得您信赖</p>
      </div>
    </el-container>
    </div>
    <el-divider></el-divider>
    <el-card class="news">
      <div class="section-title">食品安全热点</div>
      <div class="content-container">
        <button class="content-item"
                v-for="newsItem in form.news"
                :key="newsItem.id"
                @click="showNewsDetail(newsItem)">
          <el-image class="image" :src="newsItem.photo_url[0]"/>
          <div class="item-info">
            <span class="title">{{ newsItem.title }}</span>
            <span class="date">{{ newsItem.date || '未指定日期' }}</span>
          </div>
        </button>
      </div>
      <el-button @click="getAllNews" class="view-more-btn">查看更多</el-button>
    </el-card>

    <el-divider></el-divider>

    <el-card class="knowledge">
      <div class="section-title">食品安全知识</div>
      <div class="content-container">
        <button class="content-item"
                v-for="knowledgeItem in form.knowledge"
                :key="knowledgeItem.id"
                @click="showKnowledgeDetail(knowledgeItem)">
          <el-image class="image" :src="knowledgeItem.photo_url[0]"/>
          <div class="item-info">
            <span class="title">{{ knowledgeItem.title }}</span>
            <span class="date">{{ knowledgeItem.date || '未指定日期' }}</span>
          </div>
        </button>
      </div>
      <el-button @click="getAllKnowledge" class="view-more-btn">查看更多</el-button>
    </el-card>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  padding: 20px;
  height: 100%;
  background-color: #f9f9f9;
}

.home{
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;
  display: flex;
  justify-content: center;
}

.homeimage {
  width: 60%;
  height: 400px;
  object-fit: cover;
  display: block;
}

.banner-content {
  position: absolute;
  width: 30%;
  height: 400px;
  color: rgb(49, 29, 29);
  text-align: center;
  background-color: rgba(242, 200, 200, 0.5); /* 半透明黑色背景 */
  left: 20%;
}

.banner-content h1 {
  margin-bottom: 30px;
  margin-top: 150px;
  font-weight: bolder;
}

.banner-content p {
  margin-bottom: 10px;
  font-weight: bold;
}

.introduction{
  flex: 1;
}

.news,
.knowledge {
  flex: 1;
  width: 100%;
  margin-bottom: 20px;
}

.section-title {
  font-size: 1.5rem;
  font-weight: bold;
  margin-top: 20px;
  margin-bottom: 10px;
  color: #333;
  display: flex;
  justify-content: center;
}

.content-container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
}

.content-item {
  background-color: #fff;
  border-radius: 10px;
  width: 280px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  overflow: hidden;
  transition: transform 0.3s ease;
}

.content-item:hover {
  transform: translateY(-5px);
}

.image {
  width: 100%;
  height: 180px;
  object-fit: cover;
}

.item-info {
  padding: 10px;
  text-align: center;
}

.title {
  display: block;
  font-size: 1rem;
  font-weight: bold;
  color: #333;
  margin-bottom: 5px;
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;
}

.date {
  display: block;
  font-size: 0.875rem;
  color: #777;
}

.view-more-btn {
  width: 100%;
  margin-top: 20px;
  text-align: center;
  font-size: 1rem;
  background-color: #4CAF50;
  color: white;
  border-radius: 5px;
}

.view-more-btn:hover {
  background-color: #45a049;
}
</style>
