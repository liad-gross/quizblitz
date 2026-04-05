<template>
  <div>
    <h2>Create an account</h2>
    <p v-if="error" style="color: red">{{ error }}</p>
    <p v-if="success" style="color: green">{{ success }}</p>
    <input v-model="email" type="email" placeholder="Email" />
    <input v-model="password" type="password" placeholder="Password (min 6 characters)" />
    <button @click="handleRegister">Register</button>
    <p>Already have an account? <RouterLink to="/login">Log in</RouterLink></p>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useGameStore } from '@/stores/gameStore'

const store = useGameStore()
const email = ref('')
const password = ref('')
const error = ref('')
const success = ref('')

async function handleRegister() {
  try {
    await store.register(email.value, password.value)
    success.value = 'Account created! You can now log in.'
    error.value = ''
  } catch (err) {
    error.value = err.message
  }
}
</script>