<script setup>
import HelloWorld from "./components/HelloWorld.vue";
import Quiz from "./components/Quiz.vue";
import { ref, computed } from "vue";

const app_title = ref("Quiz App using Vue");
const name = ref("Dominic");
const quizCompleted = ref(false);

const questions = ref([
  {
    question: "What is the first letter of the Alphabet ?",
    answer: 2,
    options: ["B", "C", "A"],
    selected: null,
  },
  {
    question: "What is 1 + 5 ?",
    answer: 0,
    options: ["6", "4", "7"],
    selected: null,
  },
]);
const currentQuestionIndex = ref(0);

const score = computed(() => {
  let value = 0;

  questions.value.forEach((q) => {
    if (q.selected == q.answer) {
      value++;
    }
  });

  return value;
});

const setAnswer = (evt) => {
  questions.value[currentQuestionIndex.value].selected = evt.target.value;
  evt.target.value = null;
};

const retakeQuiz = () => {
  questions.value.forEach((q, index) => (questions.value[index].selected = null));
  quizCompleted.value = false;
  currentQuestionIndex.value = 0;
};
const NextQuestion = () => {
  if (currentQuestionIndex.value < questions.value.length - 1) {
    currentQuestionIndex.value++;
  } else {
    quizCompleted.value = true;
  }
};
</script>

<template>
  <div class="container">
    <h1>{{ app_title }}</h1>
    <h5>Made by {{ name }}</h5>
    <Quiz
      :retakeQuiz="retakeQuiz"
      :score="score"
      :quizCompleted="quizCompleted"
      :NextQuestion="NextQuestion"
      :setAnswer="setAnswer"
      :currentQuestionIndex="currentQuestionIndex"
      :questions="questions"
    />
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 10px;
  box-sizing: border-box;
}
h1 {
  color: yellow;
}

h5 {
  color: rgb(228, 208, 208);
}
.container {
  height: 100vh;
  width: 100vw;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  text-align: center;
  background: rgb(45, 114, 76);
}
</style>
