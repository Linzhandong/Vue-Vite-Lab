<script setup lang="ts">
import { toRefs } from 'vue'
import { type Event } from '@/types'
import { useRouter } from 'vue-router'

const props = defineProps<{
  event: Event
  id: String
}>()

// eslint-disable-next-line @typescript-eslint/no-unused-vars
const { event } = toRefs(props)
const router = useRouter()

const register = () => {
  // 模拟注册 API 调用
  console.log('Registering for event:', event.value?.title)
  
  // 如果注册 API 调用成功
  // 返回事件详情页面
  router.push({ name: 'event-detail-view' })
}
</script>

<template>
  <div class="register-view">
    <h2>Register for {{ event.title }}</h2>
    <p>Register event here - Fill out the registration form below:</p>
    
    <div class="registration-form">
      <div class="form-group">
        <label for="name">Full Name:</label>
        <input type="text" id="name" placeholder="Enter your full name">
      </div>
      
      <div class="form-group">
        <label for="email">Email:</label>
        <input type="email" id="email" placeholder="Enter your email">
      </div>
      
      <div class="form-group">
        <label for="phone">Phone:</label>
        <input type="tel" id="phone" placeholder="Enter your phone number">
      </div>
      
      <button @click="register" class="register-btn">Complete Registration</button>
    </div>
  </div>
</template>

<style scoped>
.register-view {
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
}

.registration-form {
  text-align: left;
  margin-top: 20px;
}

.form-group {
  margin-bottom: 15px;
}

.form-group label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}

.form-group input {
  width: 100%;
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 4px;
  box-sizing: border-box;
}

.register-btn {
  background-color: #42b983;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
  margin-top: 10px;
}

.register-btn:hover {
  background-color: #369c6f;
}
</style>