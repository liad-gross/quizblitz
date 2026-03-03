<template>
  <div>
    <p>{{ question.question }}</p>
    <button
      v-for="(answer, index) in question.answers"
      :key="index"
      :disabled="answered"
      :class="getClass(index)"
      @click="selectAnswer(index)"
    >
      {{ answer }}
    </button>
  </div>
</template>

<script>
export default {
  name: 'QuestionCard',
  props: {
    question: {
      type: Object,
      required: true
    }
  },
  emits: ['answer'],
  data() {
    return {
      selected: null,
      answered: false
    }
  },
  methods: {
    selectAnswer(index) {
      this.selected = index
      this.answered = true

      const isCorrect = index === this.question.correct

      setTimeout(() => {
        this.$emit('answer', isCorrect)
        this.selected = null
        this.answered = false
      }, 1000)
    },
    getClass(index) {
      if (this.selected === null) return ''
      if (index === this.question.correct) return 'correct'
      if (index === this.selected) return 'wrong'
      return ''
    }
  }
}
</script>

<style scoped>
.correct { background-color: green; color: white; }
.wrong   { background-color: red;   color: white; }
</style>