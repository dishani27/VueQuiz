<template>
  <div id="app">
    <Header :currentNum="currentNum"  />
    <b-container class="bv-example-row">
       <b-row>
         <b-col sm="6" offset="3"> 
           <QuestionBox v-bind:currentQuestion="questions[index]" :next="next" 
                        v-if="questions.length" :currentNum="currentNum" />
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
    return{
      questions: [],   //questions = json term
      index: 0,
      correctNum: 0,
      currentNum: 1
    }
  },
  methods: {
    next(){
      this.index++; 
      var item = document.querySelector("#item");
      item.className = "list-group"; 
      this.currentNum++    
    },
  },
  mounted: function(){
    fetch('https://opentdb.com/api.php?amount=10&category=18&difficulty=easy&type=multiple',  {
      method: 'get'
    }).then((response) =>{
      return response.json()
    }).then((jsonData) =>{
      this.questions = jsonData.results;
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
  margin-top: 0px;
}
body{
  background: url("assets/images/bg.jpg") 74% 67% !important;
}
</style>
