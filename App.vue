<template>
  <div id="app">
    <Tab
    :numCorrect="numCorrect"
    :numTotal="numTotal"
       />

    <QuestionBox 
    v-if="questions.length"
    :currentQuestion = "questions[index]"
    :next="next"
    :back="back"
    :increment="increment"
    />
  </div>
</template>

<script>
import Tab from './components/Tab.vue'
import QuestionBox from './components/QuestionBox.vue'


export default {
  name: 'App',
  components: {
    Tab,
    QuestionBox
  },
  data() {
    return{
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0
    }
  },
  methods: {
    next(){
      this.index++
    },
    back(){
      this.index--
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.numCorrect++
      }
      this.numTotal++
    }
  },
  mounted: function(){
    fetch('https://opentdb.com/api.php?amount=10&category=18&difficulty=easy&type=multiple',
    {
      method: 'get'
    })
    .then((response) => {
     return response.json()
     })

    .then((jsonData)=>{
     this.questions=jsonData.results})
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
