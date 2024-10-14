<script setup lang="ts">
import { ref, onMounted } from 'vue';

const username = ref('');
const password = ref('');
const captcha = ref('');
const userCaptcha = ref('');
const captchaCanvas = ref<HTMLCanvasElement | null>(null);

const generateCaptcha = () => {
  const canvas = captchaCanvas.value;
  if (!canvas) return;

  const ctx = canvas.getContext('2d');
  if (!ctx) return;

  // Clear canvas
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  // Generate random captcha
  captcha.value = Math.random().toString(36).substring(2, 8).toUpperCase();

  // Draw captcha
  ctx.font = '24px Arial';
  ctx.fillStyle = '#00838f';
  ctx.fillText(captcha.value, 10, 30);

  // Add some noise
  for (let i = 0; i < 100; i++) {
    ctx.fillStyle = `rgba(${Math.random() * 255},${Math.random() * 255},${Math.random() * 255},0.3)`;
    ctx.fillRect(Math.random() * canvas.width, Math.random() * canvas.height, 2, 2);
  }
};

const handleLogin = () => {
  if (userCaptcha.value.toUpperCase() !== captcha.value) {
    alert('验证码错误，请重新输入');
    generateCaptcha();
    userCaptcha.value = '';
    return;
  }
  // 这里添加登录逻辑
  console.log('Login attempt:', username.value, password.value);
};

onMounted(() => {
  generateCaptcha();
});
</script>

<template>
  <div class="login-container">
    <div class="tech-background">
      <div class="cube"></div>
      <div class="cube"></div>
      <div class="cube"></div>
      <div class="cube"></div>
      <div class="cube"></div>
    </div>
    <div class="login-box">
      <h2>登录</h2>
      <form @submit.prevent="handleLogin">
        <div class="input-group">
          <input type="text" v-model="username" required>
          <label>用户名</label>
        </div>
        <div class="input-group">
          <input type="password" v-model="password" required>
          <label>密码</label>
        </div>
        <div class="input-group captcha-group">
          <input type="text" v-model="userCaptcha" required>
          <label>验证码</label>
          <canvas ref="captchaCanvas" width="120" height="40" @click="generateCaptcha"></canvas>
        </div>
        <button type="submit" class="login-btn">登录</button>
      </form>
    </div>
  </div>
</template>

<style scoped>
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #e0f7fa;
  position: relative;
  overflow: hidden;
}

.tech-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
}

.cube {
  position: absolute;
  width: 80px;
  height: 80px;
  background: rgba(0, 188, 212, 0.2);
  animation: cube-animation 20s infinite linear;
}

.cube:nth-child(1) { top: 20%; left: 10%; }
.cube:nth-child(2) { top: 70%; left: 20%; animation-delay: -5s; }
.cube:nth-child(3) { top: 40%; left: 60%; animation-delay: -10s; }
.cube:nth-child(4) { top: 80%; left: 80%; animation-delay: -15s; }
.cube:nth-child(5) { top: 10%; left: 90%; animation-delay: -7s; }

@keyframes cube-animation {
  0% { transform: rotate(0deg) translateY(0); opacity: 0.7; }
  50% { transform: rotate(180deg) translateY(-100px); opacity: 0.2; }
  100% { transform: rotate(360deg) translateY(0); opacity: 0.7; }
}

.login-box {
  background: rgba(255, 255, 255, 0.9);
  padding: 40px;
  border-radius: 10px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
  width: 300px;
  z-index: 1;
}

h2 {
  text-align: center;
  color: #00bcd4;
  margin-bottom: 30px;
}

.input-group {
  position: relative;
  margin-bottom: 30px;
}

input {
  width: 100%;
  padding: 10px 0;
  font-size: 16px;
  color: #333;
  border: none;
  border-bottom: 1px solid #00bcd4;
  outline: none;
  background: transparent;
}

label {
  position: absolute;
  top: 0;
  left: 0;
  padding: 10px 0;
  font-size: 16px;
  color: #00bcd4;
  pointer-events: none;
  transition: 0.5s;
}

input:focus ~ label,
input:valid ~ label {
  top: -20px;
  left: 0;
  color: #00bcd4;
  font-size: 12px;
}

.login-btn {
  width: 100%;
  background-color: #00bcd4;
  border: none;
  padding: 10px;
  color: #fff;
  font-size: 16px;
  cursor: pointer;
  border-radius: 5px;
  transition: background-color 0.3s;
}

.login-btn:hover {
  background-color: #0097a7;
}

.captcha-group {
  display: flex;
  align-items: center;
}

.captcha-group input {
  width: calc(100% - 130px);
  margin-right: 10px;
}

.captcha-group canvas {
  cursor: pointer;
  border: 1px solid #00bcd4;
  border-radius: 4px;
}
</style>