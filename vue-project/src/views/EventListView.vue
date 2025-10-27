<!-- EventListView.vue -->
<script setup lang="ts">
import EventCard from '@/components/EventCard.vue'
import { type Event } from '@/types'
import { ref, onMounted, computed, watchEffect } from 'vue'
import EventService from '@/services/EventService'
import { useRouter } from 'vue-router'

const events = ref<Event[] | null>(null)
const totalEvents = ref(0)
const router = useRouter()

const props = defineProps({
  page: {
    type: Number,
    required: true,
  },
  size: {
    // 恢复 size prop
    type: Number,
    required: true,
  },
})

const page = computed(() => props.page)
const size = computed(() => props.size)

const hasNextPage = computed(() => {
  const totalPages = Math.ceil(totalEvents.value / size.value)
  return page.value < totalPages
})

onMounted(() => {
  watchEffect(() => {
    EventService.getEvents(size.value, page.value)
      .then((response) => {
        events.value = response.data
        totalEvents.value = response.headers['x-total-count']
      })
      .catch((error) => {
        console.error('There was an error!', error)
        router.push({ name: 'network-error-view' })
      })
  })
})
</script>

<!-- EventListView.vue -->
<template>
  <div>
    <h1>Events For Good</h1>
    <div class="events">
      <EventCard v-for="event in events" :key="event.id" :event="event" />
    </div>
    <div class="pagination">
      <RouterLink
        id="page-prev"
        :to="{ name: 'event-list-view', query: { page: page - 1, size: size } }"
        rel="prev"
        v-if="page != 1"
      >
        &lt; Prev Page
      </RouterLink>
      <RouterLink
        id="page-next"
        :to="{ name: 'event-list-view', query: { page: page + 1, size: size } }"
        rel="next"
        v-if="hasNextPage"
      >
        Next Page &gt;
      </RouterLink>
    </div>
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.pagination {
  display: flex;
  width: 290px;
  margin: 0 auto;
}

.pagination a {
  flex: 1;
  text-decoration: none;
  color: #2c3e50;
}

#page-prev {
  text-align: left;
}

#page-next {
  text-align: right;
}
</style>
