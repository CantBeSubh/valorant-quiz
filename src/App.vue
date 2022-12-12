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
import * as data from "../public/questions.json";
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
    this.questions = data;
  },
};
</script>

<style>
* {
  font-family: "Verdana", cursive, sans-serif;
  color: #ffffff;

}

body {
  margin: 0;
  padding: 0;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  user-select: none;

  background-color: #222;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

.container {
  background-color: #567;
  width: 450px;
  min-height: 200px;
  height: min-content;
  border-radius: 15px;
  padding: 20px;
  box-shadow: 10px 10px 42px 0px rgba(0, 68, 255, 0.8);
  display: flex;
  justify-content: space-evenly;
  animation: yt-effect 6s ease-in-out infinite;
}

@keyframes yt-effect {
  0% {
    box-shadow: 0px 0px 25px rgba(0, 68, 255, 0.8);
  }

  50% {
    box-shadow: 0px 0px 200px rgba(0, 68, 255, 0.8);
  }

  100% {
    box-shadow: 0px 0px 25px rgba(0, 68, 255, 0.8);
  }
}

.score-section {
  display: flex;
  font-size: 24px;
  align-items: center;
}

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

.answer-section {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
</style>
