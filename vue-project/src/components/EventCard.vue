<!-- EventCard.vue -->
<script setup lang="ts">
import { type Event } from '@/types'
import EventInfo from './EventInfo.vue'

defineProps<{
  event: Event | null  // 允许 event 为 null
}>()
</script>

<template>
  <RouterLink
    v-if="event"
    class="event-link"
    :to="{ name: 'event-detail-view', params: { id: event.id } }"
  >
    <div class="cursor-pointer border border-gray-600 p-[20px] w-[250px] mb-[18px] hover:scale-101 hover:shadow-sp">
      <h2>{{ event.title }}</h2>
      <span>@{{ event.time }} on {{ event.date }}</span>
      <EventInfo :event="event" />
    </div>
  </RouterLink>
  <div v-else class="cursor-pointer border border-gray-600 p-4 w-64 mb-6 bg-gray-100">
    <h2>Loading...</h2>
  </div>
</template>

<style scoped>
.event-link {
  text-decoration: none;
  color: #2c3e50;
}
</style>
