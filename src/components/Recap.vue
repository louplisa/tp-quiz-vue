<template>
  <h1>Recap</h1>
  <p>
    {{ hasWon ? quiz.success_message : quiz.failer_message}}
  </p>
  <p>
    Score : {{ score }}/{{ quiz.questions.length }}
  </p>
</template>

<script setup>
import {computed} from "vue";

const props =defineProps({
  quiz: Object,
  answers: Array
})
const score = computed(() => {
  return props.quiz.questions.reduce((accumulator, question, k) => {
    if (question.correct_answer === props.answers[k]) {
      return accumulator + 1
    }
    return accumulator
  }, 0)
})

const hasWon = computed(() => score.value >= props.quiz.minimum_score)
</script>