<template>
  <div class="app">
    <h1 class="title">🎯 Vue Quiz App</h1>
    <Quiz />
  </div>
</template>

<script setup>
import Quiz from './components/Quiz.vue'
</script>

<style>
.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 30px;
  font-family: "Segoe UI", sans-serif;
  background: #f4f7fb;
  min-height: 100vh;
}
.title {
  font-size: 2.5rem;
  margin-bottom: 20px;
  color: #2c3e50;
}
</style>
