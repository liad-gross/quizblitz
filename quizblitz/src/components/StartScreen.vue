<template>
  <div>
    <h1>QuizBlitz</h1>
    <p>Test your web dev knowledge across 10 questions.</p>
    <button @click="$emit('start')">Play</button>
  </div>
</template>

<script>
export default {
  name: 'StartScreen',
  emits: ['start']
}
</script>