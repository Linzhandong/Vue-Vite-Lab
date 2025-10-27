<!-- views/event/DetailView.vue -->
<script setup lang="ts">
import { toRefs, defineProps, onMounted, ref } from 'vue'
import { type Event } from '@/types'
import { useMessageStore } from '@/stores/message'
import { storeToRefs } from 'pinia'

const props = defineProps<{
  event: Event
  id: string
}>()

const { event } = toRefs(props)
const store = useMessageStore()
const { message } = storeToRefs(store)

// 本地消息状态，用于在详情组件内部显示
const localMessage = ref('')

// 监听全局消息变化，如果是编辑相关的消息，在本地显示
onMounted(() => {
  if (message.value && message.value.includes('updated')) {
    localMessage.value = message.value
    // 3秒后清除本地消息
    setTimeout(() => {
      localMessage.value = ''
    }, 3000)
  }
})
</script>

<template>
  <div class="detail-view">
    <div v-if="localMessage" class="edit-success-message">
      <p>{{ localMessage }}</p>
    </div>

    <div class="event-details">
      <p><strong>Time:</strong> {{ event.time }} on {{ event.date }}</p>
      <p><strong>Location:</strong> {{ event.location }}</p>
      <p><strong>Description:</strong> {{ event.description }}</p>
      <p><strong>Category:</strong> {{ event.category }}</p>
      <p><strong>Organizer:</strong> {{ event.organizer }}</p>
      <p><strong>Pets Allowed:</strong> {{ event.petsAllowed ? 'Yes' : 'No' }}</p>
    </div>
  </div>
</template>

<style scoped>
.detail-view {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  text-align: left;
}

.edit-success-message {
  background-color: #d4edda;
  border: 1px solid #c3e6cb;
  border-radius: 4px;
  padding: 12px;
  margin-bottom: 20px;
  color: #155724;
}

.edit-success-message p {
  margin: 0;
  font-weight: bold;
}

.event-details {
  background-color: #f8f9fa;
  padding: 20px;
  border-radius: 8px;
  border: 1px solid #e9ecef;
}

.event-details p {
  margin-bottom: 10px;
  line-height: 1.5;
}

.event-details strong {
  color: #2c3e50;
}
</style>
