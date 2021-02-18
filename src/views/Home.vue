<template>
  <div class="about">
    <Navbar
            :correct="correctAnswer"
            :wrong="wrongAnswer"
            :questionsNumber="index"
            :total="questions.length"
    />

    <div class="container">
      <template v-for="(question, key) in questions">
        <Question
                v-if="key === index"
                :question="question"
                :next="nextQuestion"
                :correct="increaseCorrectAnswer"
                :wrong="increaseWrongAnswer"
        />
      </template>
    </div>
  </div>
</template>

<script>

  import Navbar from "@/components/Navbar";
  import Question from "../components/Question";

  export default {
    name: 'Home',
    components: {
      Navbar,
      Question
    },
    data() {
      return {
        questions: [],
        questionNumbers: 0,
        correctAnswer: 0,
        wrongAnswer: 0,
        index: 0,
      }
    },
    methods: {
      nextQuestion() {
        if(this.index < this.questions.length - 1){
          this.index++;
        }
        // console.log(this.questions)
      },

      increaseCorrectAnswer() {
        this.correctAnswer++;
      },

      increaseWrongAnswer() {
        this.wrongAnswer++;
      }
    },
    created() {
      fetch('https://opentdb.com/api.php?amount=10&category=21&type=multiple', {
        method: 'get'
      })
              .then(response => response.json())
              .then(response => this.questions = response.results);

    },
  }
</script>