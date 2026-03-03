<template>
  <div>
    <h2>Game Over</h2>
    <p>You scored {{ score }} out of 10</p>
    <button @click="$emit('restart')">Play Again</button>
  </div>
</template>

<script>
export default {
  name: 'ScoreBoard',
  props: {
    score: Number
  },
  emits: ['restart']
}
</script>