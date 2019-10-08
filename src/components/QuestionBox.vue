<template>
  <div class="question-box-container">
    <b-jumbotron>
      <template v-slot:lead>
        {{currentQuestion.question}}
      </template>

      <hr class="my-4">
      <b-list-group>
        <b-list-group-item
        v-for ="(answer, index) in answers" :key="index"
        @click="selectedAnswer(index)"
        :class="[selectedIndex === index ? 'selected' :  '']"
        >
          {{answer}}
          </b-list-group-item>
      </b-list-group>

      <b-button variant="primary" href="#">Submit</b-button>
      <b-button variant="success" @click="nextQuestion" class="ml-3">Next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
  import _ from 'lodash'
  export default {
    props: {
      currentQuestion: Object,
      nextQuestion: Function
    },
    data(){
      return {
        selectedIndex : null,
        shuffledAnswers : [],
      }
    },
    computed: {
      answers(){
      let answers = [...this.currentQuestion.incorrect_answers]
        answers.push(this.currentQuestion.correct_answer)
        return answers
      }
    },
    watch: {
      currentQuestion(){
        this.selectedIndex = null
        this.shuffleAnswers()
      }
    },
    methods: {
      selectedAnswer(index){
        this.selectedIndex= index
      },
      shuffleAnswers(){
        let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
      }
    },
    mounted(){
      console.log(this.currentQuestion.correct_answer)
    }    
  }
</script>

<style  scoped>
.list-group{
margin-bottom: 20px;
}
.list-group-item:hover{
  background: #eee;
  cursor:pointer;
}
.selected{
  background-color: lightblue;
}
.correct{
  background-color: lightgreen;
}
.incorrect{
  background-color:red;
}
</style>
