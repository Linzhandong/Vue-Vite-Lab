<script setup lang="ts">
import { RouterLink, RouterView, useRouter } from 'vue-router'
import { ref, watch } from 'vue'

const router = useRouter()
const pageSize = ref(2)

// 当页面大小改变时，更新路由
watch(pageSize, (newSize) => {
  router.push({ 
    name: 'event-list-view', 
    query: { 
      page: 1, // 重置到第一页
      size: newSize 
    } 
  })
})
</script>

<template>
  <div id="layout">
    <header>
      <div class="wrapper">
        <nav>
          <RouterLink :to="{ name: 'event-list-view' }">Event</RouterLink> |
          <RouterLink :to="{ name: 'students' }">Students</RouterLink> |
          <RouterLink :to="{ name: 'about' }">About</RouterLink>
        </nav>
        <div class="page-size-selector">
          <label for="pageSize">Events per page: </label>
          <select id="pageSize" v-model="pageSize">
            <option value="2">2</option>
            <option value="4">4</option>
            <option value="6">6</option>
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
</style>