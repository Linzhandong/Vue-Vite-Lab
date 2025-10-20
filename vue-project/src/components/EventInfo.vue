<script setup lang="ts">
import type { Event } from '@/types'

defineProps<{
  event: Event
}>()
</script>

<template>
  <div class="event-info">
    <div class="category">{{ event.category }}</div>
    <div class="organizer">{{ event.organizer }}</div>
  </div>
</template>

<style scoped>
.event-info {
  font-size: 14px;
  text-align: right;
  margin-top: 10px;
}

.category, .organizer {
  font-size: 14px;
}
</style>