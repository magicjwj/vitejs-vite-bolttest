<script setup lang="ts">
import { ref } from 'vue'
import HelloWorld from './components/HelloWorld.vue'
import LoginPage from './components/LoginPage.vue'

const showLogin = ref(true)

const toggleView = () => {
  showLogin.value = !showLogin.value
}
</script>

<template>
  <div>
    <button @click="toggleView" class="toggle-btn">
      {{ showLogin ? '显示主页' : '显示登录' }}
    </button>
    <LoginPage v-if="showLogin" />
    <div v-else>
      <a href="https://vite.dev" target="_blank">
        <img src="/vite.svg" class="logo" alt="Vite logo" />
      </a>
      <a href="https://vuejs.org/" target="_blank">
        <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
      </a>
      <HelloWorld msg="Vite + Vue" />
    </div>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
.toggle-btn {
  position: fixed;
  top: 10px;
  right: 10px;
  z-index: 1000;
  padding: 10px 20px;
  background-color: #00bcd4;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}
.toggle-btn:hover {
  background-color: #0097a7;
}
</style>