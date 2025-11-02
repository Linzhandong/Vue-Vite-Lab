<!-- EventInfo.vue -->
<script setup lang="ts">
import type { Event } from '@/types'

defineProps<{
  event: Event
}>()
</script>

<template>
  <div class="text-sm text-right mt-2.5">
    <div class="text-sm">{{ event.category }}</div>
    <div class="text-sm">{{ event.organizer }}</div>
  </div>
</template>

<style scoped>

</style>
