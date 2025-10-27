<!-- views/event/LayoutView.vue -->
<script setup lang="ts">
import { useEventStore } from '@/stores/event'
import { storeToRefs } from 'pinia'

const store = useEventStore()
const { event } = storeToRefs(store)
</script>

<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <nav>
      <RouterLink :to="{ name: 'event-detail-view' }">Details</RouterLink> |
      <RouterLink :to="{ name: 'event-register-view' }">Register</RouterLink> |
      <RouterLink :to="{ name: 'event-edit-view' }">Edit</RouterLink>
    </nav>
    <RouterView :event="event" />
  </div>
  <div v-else>
    <p>Loading event...</p>
  </div>
</template>

<style scoped>
nav {
  margin: 20px 0;
  padding: 10px 0;
  border-bottom: 1px solid #e0e0e0;
}

nav a {
  margin: 0 10px;
  text-decoration: none;
  color: #2c3e50;
  font-weight: 500;
}

nav a.router-link-exact-active {
  color: #42b983;
  font-weight: bold;
}

nav a:hover {
  color: #42b983;
}

h1 {
  color: #2c3e50;
  margin-bottom: 10px;
}
</style>
