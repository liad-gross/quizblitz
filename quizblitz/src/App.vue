<template>
  <div id="app">
    <StartScreen v-if="gameState === 'start'" @start="startGame" />
    <QuestionCard
      v-else-if="gameState === 'playing'"
      :question="questions[currentIndex]"
      @answer="handleAnswer"
    />
    <ScoreBoard
      v-else
      :score="score"
      @restart="resetGame"
    />
  </div>
</template>

<script>
import StartScreen from './components/StartScreen.vue'
import QuestionCard from './components/QuestionCard.vue'
import ScoreBoard from './components/ScoreBoard.vue'

export default {
  name: 'App',
  components: { StartScreen, QuestionCard, ScoreBoard },
  data() {
    return {
      gameState: 'start',
      currentIndex: 0,
      score: 0,
      questions: [
        {
          question: "What does CSS stand for?",
          answers: ["Cascading Style Sheets", "Creative Style System", "Computer Style Syntax", "Coloured Screen Sheets"],
          correct: 0
        },
        {
          question: "Which HTML tag is used to link an external JavaScript file?",
          answers: ["<js>", "<script>", "<link>", "<javascript>"],
          correct: 1
        },
        {
          question: "What does the 'V' in Vue.js stand for?",
          answers: ["Virtual", "Visual", "View", "Variable"],
          correct: 2
        },
        {
          question: "Which of the following is NOT a JavaScript data type?",
          answers: ["String", "Boolean", "Float", "Undefined"],
          correct: 2
        },
        {
          question: "In Vue 3, which directive is used for two-way data binding?",
          answers: ["v-bind", "v-on", "v-model", "v-sync"],
          correct: 2
        },
        {
          question: "What tool does Vite replace in the Vue ecosystem?",
          answers: ["Webpack + Vue CLI", "Babel", "ESLint", "npm"],
          correct: 0
        },
        {
          question: "What does HTML stand for?",
          answers: ["Hyper Text Markup Language", "High Tech Modern Language", "Hyper Transfer Meta Language", "Home Tool Markup Language"],
          correct: 0
        },
        {
          question: "Which CSS property controls the space between elements?",
          answers: ["padding", "spacing", "margin", "gap"],
          correct: 2
        },
        {
          question: "In Vue, how do you pass data from a parent to a child component?",
          answers: ["$emit", "slots", "props", "ref"],
          correct: 2
        },
        {
          question: "What does 'npm' stand for?",
          answers: ["Node Package Manager", "New Programming Module", "Node Process Monitor", "Network Package Module"],
          correct: 0
        }
      ]
    }
  },
  methods: {
    startGame() {
      this.currentIndex = 0
      this.score = 0
      this.gameState = 'playing'
    },
    handleAnswer(isCorrect) {
      if (isCorrect) this.score++
      this.currentIndex++
      if (this.currentIndex === this.questions.length) {
        this.gameState = 'end'
      }
    },
    resetGame() {
      this.gameState = 'start'
    }
  }
}
</script>