<script setup lang="ts">
import type { Student } from '@/types'

defineProps<{
  student: Student
}>()
</script>

<template>
  <div class="student-card">
    <h2>{{ student.name }} {{ student.surname }}</h2>
    <div class="gpa">GPA: {{ student.gpa }}</div>
  </div>
</template>

<style scoped>
.student-card {
  padding: 20px;
  width: 250px;
  cursor: pointer;
  border: 1px solid #39495c;
  margin-bottom: 18px;
  background-color: #f8f9fa;
}

.student-card:hover {
  transform: scale(1.01);
  box-shadow: 0 3px 12px 0 rgba(0, 0, 0, 0.2);
}

.gpa {
  font-weight: bold;
  color: #2c5aa0;
  margin-top: 10px;
}
</style>