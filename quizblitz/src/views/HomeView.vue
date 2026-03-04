<template>
  <div>
    <StartScreen @start="startGame" />
  </div>
</template>

<script>
import StartScreen from '../components/StartScreen.vue'

export default {
  name: 'HomeView',
  components: { StartScreen },
  methods: {
    startGame() {
      sessionStorage.setItem('gameStarted', 'true')
      this.$router.push({ name: 'play' })
    }
  }
}
</script>