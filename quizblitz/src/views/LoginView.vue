<template>
  <div>
    <h2>Log in</h2>
    <p v-if="error" style="color: red">{{ error }}</p>
    <input v-model="email" type="email" placeholder="Email" />
    <input v-model="password" type="password" placeholder="Password" />
    <button @click="handleLogin">Log in</button>
    <p>No account? <RouterLink to="/register">Register</RouterLink></p>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import { useGameStore } from '@/stores/gameStore'

const store = useGameStore()
const router = useRouter()
const email = ref('')
const password = ref('')
const error = ref('')

async function handleLogin() {
  try {
    await store.login(email.value, password.value)
    router.push('/')
  } catch (err) {
    error.value = err.message
  }
}
</script>