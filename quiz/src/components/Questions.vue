<template>
  <div class="questions-ctr">
    <div class="progress">
      <div
        class="bar"
        :style="{ width: `${(questionsAnswers / questions.length) * 100}%` }"
      ></div>
      <div class="status">
        {{ questionsAnswers }} out of {{ questions.length }} questions answered
      </div>
    </div>
    <transition-group name="fade">
      <div
        class="single-question"
        v-for="(question, index) in questions"
        :key="question.q"
        v-show="index === questionsAnswers"
      >
        <div class="question">{{ question.q }}</div>
        <div class="answers">
          <div
            class="answer"
            v-for="answer in question.answers"
            :key="answer.text"
            @click.prevent="selectAnswer(answer.is_correct)"
          >
            {{ answer.text }}
          </div>
        </div>
      </div>
    </transition-group>
  </div>
</template>

<script>
export default {
  props: {
    questions: {
      type: Array,
      default: () => [],
    },
    questionsAnswers: {
      type: Number,
      default: null,
    },
  },
  emits: { question_answered: null },
  methods: {
    selectAnswer(is_correct) {
      this.$emit('question_answered', is_correct);
    },
  },
};
</script>

<style></style>
