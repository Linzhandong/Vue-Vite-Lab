<!-- StudentCard.vue -->
<script setup lang="ts">
import type { Student } from '@/types'

defineProps<{
  student: Student
}>()
</script>

<template>
  <div class="p-5 w-64 cursor-pointer border border-gray-600 mb-4.5 bg-gray-50 hover:scale-101 hover:shadow-sp">
    <h2>{{ student.name }} {{ student.surname }}</h2>
    <div class="font-bold text-blue-700 mt-2.5">GPA: {{ student.gpa }}</div>
  </div>
</template>

<style scoped>

</style>
