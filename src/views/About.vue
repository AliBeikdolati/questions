<template>
  <div class="about">
    {{ hello }}
    <div>
      <input type="text" v-model="name">
      <button @click="changeName">add</button>
    </div>
    <div v-for="question in questions">{{ question.question }}</div>
  </div>
</template>

<script>
  // @ is an alias to /src
  import {mapState, mapActions} from 'vuex'

  export default {
    name: 'About',
    data() {
      return {
        name: '',
        questions: []
      }
    },
    components: {

    },
    created() {
      fetch('https://opentdb.com/api.php?amount=10&category=21&type=multiple', {
        method: 'get'
      })
              .then(response => response.json())
              .then(response => this.questions = response.results)
              .then(response => console.log(response))
    },
    computed: {
      ...mapState({
        hello: state => state.hello
      }),

    },
    methods: {
      ...mapActions([
        'addName'
      ]),
      changeName() {
        this.addName(this.name)
      }
    }
  }
</script>
