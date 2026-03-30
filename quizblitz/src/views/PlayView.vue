<template>
  <div class="play-view">

    <div class="timer-bar">
      <div
        class="timer-fill"
        :style="{ width: timerPercent + '%' }"
        :class="{ urgent: store.timeLeft <= 5 }"
      ></div>
    </div>

    <p class="progress">
      Question {{ store.progress.current }} of {{ store.progress.total }}
    </p>

    <p v-if="store.streak >= 3" class="streak">
      🔥 {{ store.streak }} in a row!
    </p>

    <QuestionCard
      v-if="store.gameState === 'playing' && store.currentQuestion"
      :question="store.currentQuestion"
      :selectedAnswer="store.selectedAnswer"
      @answer="store.submitAnswer"
    />

    <div v-else-if="store.gameState === 'end'" class="end-screen">
      <h2>Game Over</h2>
      <p>You scored {{ store.score }} of {{ store.questions.length }}</p>

      <div v-if="!store.scoreSubmitted" class="submit-score">
        <input
          v-model="store.playerName"
          placeholder="Enter your name"
          class="name-input"
        />
        <button @click="store.submitScore()" class="submit-btn">Submit Score</button>
      </div>

      <p v-else class="submitted">Score submitted!</p>

      <button @click="handleRestart" class="restart-btn">Play Again</button>
    </div>

  </div>
</template>

<script>
import { useGameStore } from '../stores/gameStore.js'
import QuestionCard from '../components/QuestionCard.vue'

export default {
  name: 'PlayView',
  components: { QuestionCard },

  setup() {
    const store = useGameStore()
    return { store }
  },

  computed: {
    timerPercent() {
      return (this.store.timeLeft / 15) * 100
    }
  },

  methods: {
    handleRestart() {
      this.store.playerName = ''
      this.store.scoreSubmitted = false
      this.store.resetGame()
      this.$router.push({ name: 'home' })
    }
  }
}
</script>

<style scoped>
.timer-bar {
  width: 100%;
  height: 8px;
  background: #333;
  border-radius: 4px;
  margin-bottom: 1rem;
  overflow: hidden;
}

.timer-fill {
  height: 100%;
  background: #4caf50;
  transition: width 0.9s linear;
}

.timer-fill.urgent {
  background: #e53935;
}

.progress {
  text-align: center;
  color: #aaa;
  margin-bottom: 1rem;
}

.streak {
  text-align: center;
  font-weight: bold;
  color: #f5c518;
  font-size: 1.2rem;
}

.end-screen {
  text-align: center;
  margin-top: 2rem;
}

.submit-score {
  display: flex;
  gap: 8px;
  justify-content: center;
  margin: 1rem 0;
}

.name-input {
  padding: 8px 12px;
  border-radius: 6px;
  border: 1px solid #444;
  background: #1e1e1e;
  color: white;
  font-size: 1rem;
}

.submit-btn, .restart-btn {
  padding: 8px 16px;
  border-radius: 6px;
  border: none;
  cursor: pointer;
  font-size: 1rem;
}

.submit-btn {
  background: #4caf50;
  color: white;
}

.restart-btn {
  background: #333;
  color: white;
  margin-top: 1rem;
  display: block;
  margin-left: auto;
  margin-right: auto;
}

.submitted {
  color: #4caf50;
  margin: 1rem 0;
}
</style>