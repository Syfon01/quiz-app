<template>
  <div id="app">
    <Header />

    <b-container class="bv-example-row mt-4">
      <b-row>
        <b-col sm="6" class="mx-auto">
          <QuestionBox
          v-if ="questions.length"
          :currentQuestion="questions[index]"
          :nextQuestion="nextQuestion"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'


export default {
  name: 'app',
  components: {
    Header,
    QuestionBox
  },
  data(){
    return {
      questions: [],
      index: 0,
    }
  },
  methods: {
    nextQuestion() {
      this.index++
    }
  },
  mounted(){
    fetch('https://opentdb.com/api.php?amount=10&category=9&type=multiple',{
      method: 'get'
    })
    .then((response) =>{
      return(response.json())
    })
    .then((jsonData) =>{
      this.questions = jsonData.results
    })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
