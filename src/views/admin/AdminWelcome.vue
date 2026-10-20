<template>
    <div class="welcome-container">
      <div class="welcome-header">
        <h1>欢迎回来，管理员！</h1>
      </div>
    </div>
</template>
  
<style scoped>
  /* 容器样式 */
.welcome-container {
    position: relative;
    display: flex;
    height: 100%;
    width: 100%;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background-color: #f9f9f9;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    overflow: hidden;
}

.welcome-container::before {
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

.welcome-header {
  position: relative;
  z-index: 1;
}

.welcome-header h1 {
    font-size: 7rem;
    color: #2b5b66;
    font-family: KaiTi;
}
</style>
  