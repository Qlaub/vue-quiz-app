<script setup>
  import q from './data/quizzes.json'
  import { ref, watch } from 'vue'
  import Card from './components/Card.vue'

  const quizzes = ref(q)
  const search = ref('')

  function updateQuizzes() {
    quizzes.value = q.filter(quiz => quiz.name.toLowerCase().includes(search.value.toLowerCase()))
  }

  watch(search, updateQuizzes)
</script>

<template>
  <div class="container">
    <header>
      <h1>Quizzes</h1>
      <input v-model.trim="search" type="text" placeholder="Search...">
    </header>
    <div class="options-container">
      <Card v-for="quiz in quizzes" :id="quiz.id" :quiz="quiz" />
    </div>
  </div>
</template>

<style scoped>
  .container {
    max-width: 1000px;
    margin: 0 auto;
  }

  header {
    margin-bottom: 30px;
    margin-top: 10px;
    display: flex;
    align-items: center;
  }

  header h1 {
    font-weight: bold;
    margin-right: 30px;
  }

  header input {
    border: none;
    background-color: rgba(128, 128, 128, 0.1);
    padding: 10px;
    border-radius: 5px;
  }

  .options-container {
    display: flex;
    flex-wrap: wrap;
    margin-top: 40px;
  }

  /* CARD */

  .card {
    width: 310px;
    overflow: hidden;
    border-radius: 2%;
    box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.1);
    margin-bottom: 35px;
    margin-right: 20px;
    cursor: pointer;
    font-size: 0px;
  }

  .card img {
    width: 100%;
    height: 190px;
    margin: 0;
  }

  .card .card-text {
    padding: 0 5px 5px 5px;
  }

  .card .card-text h2 {
    font-weight: bold;
    font-size: 24px;
  }

  .card .card-text p {
    font-size: 14px;
  }
</style>