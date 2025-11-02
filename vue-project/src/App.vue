<!-- App.vue -->
<script setup lang="ts">
import { RouterLink, RouterView, useRouter } from 'vue-router'
import { ref, watch, onMounted } from 'vue'
import { useMessageStore } from '@/stores/message'
import { storeToRefs } from 'pinia'

const router = useRouter()
const pageSize = ref(3)
const store = useMessageStore()
const { message } = storeToRefs(store)

// 添加测试
onMounted(() => {
  console.log('🚀 App.vue mounted successfully!')
  console.log('📦 Message store:', store)
  console.log('🔗 Router:', router)
})

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
  <div class="text-center font-sans text-gray-700 antialiased">
    <SpeedInsights />
    <header>
      <div id="flashMessage" class="animate-fade" v-if="message">
        <h4>{{ message }}</h4>
      </div>
      <h1>Deploy with Vercel</h1>
      <div class="wrapper">
        <nav class="py-6">
          <RouterLink
            class="font-bold text-gray-700"
            exact-active-class="text-green-500"
            :to="{ name: 'event-list-view' }"
          >
            Event
          </RouterLink> |
          <RouterLink
            class="font-bold text-gray-700"
            exact-active-class="text-green-500"
            :to="{ name: 'students' }"
          >
            Students
          </RouterLink> |
          <RouterLink
            class="font-bold text-gray-700"
            exact-active-class="text-green-500"
            :to="{ name: 'about' }"
          >
            About
          </RouterLink>
        </nav>
        <div class="page-size-selector">
          <label for="pageSize">Events per page: </label>
          <select id="pageSize" v-model="pageSize">
            <option value="3">3</option>
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
</style>
