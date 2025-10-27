<!-- App.vue -->
<script setup lang="ts">
import { RouterLink, RouterView, useRouter } from 'vue-router'
import { ref, watch } from 'vue'
import { useMessageStore } from '@/stores/message'
import { storeToRefs } from 'pinia'

const router = useRouter()
const pageSize = ref(3) // 默认值改为 3
const store = useMessageStore()
const { message } = storeToRefs(store)

// 当页面大小改变时，更新路由
watch(pageSize, (newSize) => {
  router.push({
    name: 'event-list-view',
    query: {
      page: 1, // 重置到第一页
      size: newSize,
    },
  })
})
</script>

<template>
  <div id="layout">
    <header>
      <div id="flashMessage" v-if="message">
        <h4>{{ message }}</h4>
      </div>
      <div class="wrapper">
        <nav>
          <RouterLink :to="{ name: 'event-list-view' }">Event</RouterLink> |
          <RouterLink :to="{ name: 'students' }">Students</RouterLink> |
          <RouterLink :to="{ name: 'about' }">About</RouterLink>
        </nav>
        <div class="page-size-selector">
          <label for="pageSize">Events per page: </label>
          <select id="pageSize" v-model="pageSize">
            <option value="3">3</option>
            <!-- 改为 3 -->
            <option value="6">6</option>
            <option value="9">9</option>
          </select>
        </div>
      </div>
    </header>

    <RouterView />
  </div>
</template>

<style>
#layout {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}

h2 {
  font-size: 20px;
}

.page-size-selector {
  margin-top: 10px;
}

.page-size-selector select {
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

@keyframes yellofade {
  from {
    background-color: yellow;
  }
  to {
    background-color: transparent;
  }
}

#flashMessage {
  animation: yellofade 3s ease-in-out;
}
</style>
