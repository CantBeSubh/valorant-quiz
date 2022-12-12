<template>
  <div class="container">
    <div v-if="showScore" class="score-section">
      You scored {{ score }} out of {{ questions.length }}
    </div>

    <div v-else>
      <div class="question-section">
        <div class="question-count">
          <span>Question {{ currentQuestion + 1 }}</span>/{{ questions.length }}
        </div>

        <div class="question-text">
          {{ questions[currentQuestion].question }}
        </div>
      </div>

      <div class="answer-section">
        <Options :options="questions[currentQuestion].answers" @opt-click="handleClick" />
      </div>
    </div>
  </div>
</template>

<script>
import Options from "./components/Options.vue";
export default {
  name: "App",
  components: {
    Options,
  },
  methods: {
    handleClick(correct) {
      if (correct) {
        this.score++;
      }
      this.currentQuestion++;
      if (this.currentQuestion >= this.questions.length) {
        this.showScore = true;
      }
    }
  },
  data() {
    return {
      questions: [],
      currentQuestion: 0,
      showScore: false,
      score: 0,
    };
  },
  created() {
    this.questions = [
      {
        question: "What is 2 + 2?",
        answers: [
          { id: 1, text: "4", correct: true },
          { id: 2, text: "22", correct: false },
        ],
      },
      {
        question: "What is 3 * 3?",
        answers: [
          { id: 3, text: "9", correct: true },
          { id: 4, text: "33", correct: false },
        ],
      },
    ];
  },
};
</script>

<style>
body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen",
    "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue",
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

* {
  font-family: "Verdana", cursive, sans-serif;
  color: #ffffff;
}

body {
  background-color: #7cc6fe;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

.container {
  background-color: #252d4a;
  width: 450px;
  min-height: 200px;
  height: min-content;
  border-radius: 15px;
  padding: 20px;
  box-shadow: 10px 10px 42px 0px rgba(0, 0, 0, 0.75);
  display: flex;
  justify-content: space-evenly;
}

.score-section {
  display: flex;
  font-size: 24px;
  align-items: center;
}

/* QUESTION/TIMER/LEFT SECTION */
.question-section {
  width: 100%;
  position: relative;
}

.question-count {
  margin-bottom: 20px;
}

.question-count span {
  font-size: 28px;
}

.question-text {
  margin-bottom: 12px;
}

.timer-text {
  background: rgb(230, 153, 12);
  padding: 15px;
  margin-top: 20px;
  margin-right: 20px;
  border: 5px solid rgb(255, 189, 67);
  border-radius: 15px;
  text-align: center;
}

/* ANSWERS/RIGHT SECTION */
.answer-section {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

button {
  width: 100%;
  font-size: 16px;
  color: #ffffff;
  background-color: #252d4a;
  border-radius: 15px;
  display: flex;
  padding: 5px;
  justify-content: flex-start;
  align-items: center;
  border: 5px solid #234668;
  cursor: pointer;
}

.correct {
  background-color: #2f922f;
}

.incorrect {
  background-color: #ff3333;
}

button:hover {
  background-color: #555e7d;
}

button:focus {
  outline: none;
}

button svg {
  margin-right: 5px;
}
</style>
