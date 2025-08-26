<template>
  <div class="quiz-card" v-if="!finished">
    <div v-if="loading">Loading quiz...</div>
    <div v-else>
      <div class="progress">
        Question {{ currentIndex + 1 }} / {{ questions.length }}
      </div>

      <Question
        :question="questions[currentIndex]"
        :index="currentIndex"
        @answer="handleAnswer"
      />
    </div>
  </div>

  <div v-else class="result-card">
    <h2>🎉 Quiz Completed!</h2>
    <p>You scored <strong>{{ score }}</strong> out of <strong>{{ questions.length }}</strong></p>
    <p class="percentage">({{ Math.round((score / questions.length) * 100) }}%)</p>
    <button class="restart-btn" @click="restartQuiz">Restart Quiz</button>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import Question from './Question.vue'

const questions = ref([])
const loading = ref(true)
const score = ref(0)
const currentIndex = ref(0)
const finished = ref(false)

const handleAnswer = (correct) => {
  if (correct) score.value++
  if (currentIndex.value < questions.value.length - 1) {
    currentIndex.value++
  } else {
    finished.value = true
  }
}

const restartQuiz = () => {
  score.value = 0
  currentIndex.value = 0
  finished.value = false
}

onMounted(async () => {
  const res = await fetch('https://jsonplaceholder.typicode.com/posts?_limit=5')
  const data = await res.json()

  questions.value = data.map((post, i) => ({
    id: post.id,
    title: post.title,
    options: [
      post.body.split(' ')[0],
      'Vue.js',
      'React',
      'Angular'
    ],
    answer: 'Vue.js'
  }))

  loading.value = false
})
</script>

<style scoped>
.quiz-card, .result-card {
  background: white;
  padding: 25px;
  border-radius: 15px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  width: 450px;
  text-align: center;
  margin-top: 20px;
}
.progress {
  margin-bottom: 15px;
  font-size: 1rem;
  color: #555;
}
.result-card h2 {
  color: #27ae60;
}
.percentage {
  font-size: 1.2rem;
  margin: 10px 0;
}
.restart-btn {
  margin-top: 15px;
  background: #3498db;
  border: none;
  padding: 10px 18px;
  border-radius: 8px;
  color: white;
  font-weight: bold;
  cursor: pointer;
  transition: 0.3s;
}
.restart-btn:hover {
  background: #2980b9;
}
</style>
