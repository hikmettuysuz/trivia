<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Header />
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <Question
          v-if="questions.length"
          :currentQuestion="questions[index]"
          :next="next"
          :previous="previous"
          />
        </b-col>

      </b-row>
    </b-container>

  </div>
</template>

<script>
import Header from './components/Header.vue'
import Question from './components/Question.vue'
export default {
  name: 'app',
  components: {
    Header,
    Question
  },
  data(){
    return {
      questions: [],
      index: 0
    }
  },
  methods: {
    next()
    {
      console.log(this.questions.length);
      if(this.index >= this.questions.length - 1){
        return false;
      }else {
        this.index++
      }
    },
    previous(){
      if(this.index <= 0 ){
        return false
      }else{
        this.index--
      }
    }
  },
  mounted() {
  fetch('https://opentdb.com/api.php?amount=10',{
    method:'get'
    }).then((response) => {
      return response.json()
    }).then((jsonData)=>{
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
