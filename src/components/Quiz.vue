<script setup>
import { ref } from "vue";

defineProps({
  questions: Array,
  quizCompleted: Boolean,
  currentQuestionIndex: Number,
  score: Number,
  setAnswer: Function,
  NextQuestion: Function,
  retakeQuiz: Function,
});
</script>

<template>
  <div class="QuizQuestion">
    <div class="QuizBody" v-if="!quizCompleted">
      <h4>Quiz Number {{ currentQuestionIndex + 1 }}</h4>
      <p>score : {{ score }} / {{ questions.length }}</p>
      <h2>{{ questions[currentQuestionIndex].question }}</h2>

      <div class="options">
        <label
          :class="`option ${
            questions[currentQuestionIndex].selected == index ? (index === questions[currentQuestionIndex].answer ? 'correct' : 'wrong') : ''
          }
          ${questions[currentQuestionIndex].selected != null && index != questions[currentQuestionIndex].selected ? 'disabled' : ''}
      `"
          v-for="(option, index) in questions[currentQuestionIndex].options"
          :key="index"
        >
          <input
            type="radio"
            .name="questions[currentQuestionIndex].options[index]"
            :index="index"
            :value="index"
            v-model="questions[currentQuestionIndex].selected"
            :disabled="questions[currentQuestionIndex].selected != null"
            @click="setAnswer"
          />
          <span>{{ option }}</span>
        </label>
      </div>

      <button id="btn" @click="NextQuestion" :disabled="questions[currentQuestionIndex].selected === null">
        {{
          currentQuestionIndex == questions.length - 1
            ? "FINISH"
            : questions[currentQuestionIndex].selected == null
            ? "SELECT AN OPTION"
            : "NEXT QUESTION"
        }}
      </button>
    </div>

    <div v-else>
      <h2>Congratulations. You are done with Quiz!</h2>
      <h4>score : {{ score }} / {{ questions.length }}</h4>

      <button @click="retakeQuiz">Retake</button>
    </div>
    <div></div>
  </div>
</template>

<style scoped>
.options {
  justify-self: center;
  align-self: center;
  min-height: 5rem;
  min-width: 15rem;
  display: flex;
  flex-direction: column;
  gap: 2rem;
  padding: 2rem 1rem;
}

.option {
  background: yellow;
  color: rgb(92, 82, 27);
  font-weight: bold;
  text-align: center;
  min-width: 100%;
  border-radius: 5px;
  height: 2rem;
  display: flex;
  justify-content: center;
  align-items: center;
}
.correct {
  background-color: rgb(26, 212, 26);
}

.wrong {
  background-color: rgb(197, 58, 34);
}

.disabled {
  opacity: 50%;
}

.options label:hover {
  cursor: pointer;
  transition: all 0.5s ease;
  color: rgb(245, 247, 243);
}

input[type="radio"] {
  -webkit-appearance: none;
  appearance: none;
  margin: 0;
  padding: 0;
}
.QuizBody {
  display: flex;
  flex-direction: column;
}
#btn {
  width: 12rem;
  justify-self: center;
  align-self: center;
}
</style>
