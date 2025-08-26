<template>
  <div class="question-box">
    <h3>Q{{ index + 1 }}: {{ question.title }}</h3>

    <div class="options">
      <button
        v-for="opt in question.options"
        :key="opt"
        @click="selectAnswer(opt)"
        class="option-btn"
      >
        {{ opt }}
      </button>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  question: Object,
  index: Number
})

const emit = defineEmits(['answer'])

const selectAnswer = (opt) => {
  const correct = opt === props.question.answer
  emit('answer', correct)
}
</script>

<style scoped>
.question-box h3 {
  margin-bottom: 15px;
  color: #2c3e50;
}
.options {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.option-btn {
  padding: 12px;
  background: #ecf0f1;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: 0.3s;
  font-size: 1rem;
}
.option-btn:hover {
  background: #3498db;
  color: white;
}
</style>
