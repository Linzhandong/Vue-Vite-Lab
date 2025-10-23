<script setup lang="ts">
import { defineProps, withDefaults } from 'vue'

const props = withDefaults(
  defineProps<{
    resource: string
  }>(),
  {
    resource: 'page'
  }
)
</script>

<template>
  <div class="not-found">
    <h1>Oops!</h1>
    <h3>The {{ resource }} you're looking for is not here.</h3>
    <p>We couldn't find the resource you were looking for.</p>
    <RouterLink :to="{ name: 'event-list-view' }" class="back-link">Back to the home page</RouterLink>
  </div>
</template>

<style scoped>
.not-found {
  padding: 40px;
  text-align: center;
}

.not-found h1 {
  font-size: 48px;
  color: #e74c3c;
  margin-bottom: 20px;
}

.not-found h3 {
  font-size: 24px;
  color: #2c3e50;
  margin-bottom: 15px;
}

.not-found p {
  font-size: 16px;
  color: #7f8c8d;
  margin-bottom: 25px;
}

.back-link {
  display: inline-block;
  padding: 10px 20px;
  background-color: #42b983;
  color: white;
  text-decoration: none;
  border-radius: 4px;
  font-weight: bold;
}

.back-link:hover {
  background-color: #369c6f;
}
</style>