<template>
  <div class="questions-ctr">
    <div class="progress">
      <div class="bar" :style="statusBarWidth"></div>
      <div class="status">{{ statusBarText }}</div>
    </div>
    <div
      class="single-question"
      v-for="(question, index) in questions"
      :key="question.q"
      :questionsAnswered="questionsAnswered"
    >
      <template v-if="questionsAnswered === index">
        <div class="question">{{ question.q }}</div>
        <div class="answers">
          <button
            class="answer"
            v-for="answer in question.answers"
            :key="answer.text"
            @click.prevent="selectAnswer(answer.is_correct)"
          >
            {{ answer.text }}
          </button>
        </div>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  name: "AppQuestions",

  props: {
    questions: {
      type: Array,
      required: true
    },
    questionsAnswered: {
      type: Number,
      required: true
    }
  },

  emits: ["question-answered"],

  computed: {
    statusBarText() {
      return `${this.questionsAnswered} out of ${this.questions.length} questions answered`;
    },
    statusBarWidth() {
      return {
        width: `${(this.questionsAnswered / this.questions.length) * 100}%`
      };
    }
  },

  methods: {
    selectAnswer(isCorrect) {
      this.$emit("question-answered", isCorrect);
    }
  }
};
</script>
