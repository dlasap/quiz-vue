<script setup>
import { ref } from "vue";

defineProps({
  msg: String,
  fname: String,
  lname: String,
  questions: Array,
  quizCompleted: Boolean,
});

const count = ref(0);
</script>

<template>
  <h3>{{ `${fname} ${lname} ${questions[0]} ${quizCompleted}` }}</h3>

  <div class="card">
    count is {{ count }}
    <br />
    <button type="button" @click="count++">+</button>
    <button type="button" @click="count--">-</button>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
