<template>
<div id="parent">
  <b-jumbotron id="jumbo">
    <template slot="lead">
      {{currentQuestion.question}}
    </template>
    <!-- question = json term -->
    <hr class="my-4">

    <b-list-group id="item">
       <b-list-group-item v-for="(answer, index) in this.shuffledAns"
                          v-bind:key="index" v-on:click="select(index)"
                          v-bind:class="{'incorrect': correctIndex!==selectedIndex && selectedIndex=== index, 'correct': answered && correctIndex=== index}"
                          >
                   <!-- or make a func as :class="ansClass(index)" and use if else        -->
           {{answer}} 
        </b-list-group-item>
    </b-list-group>

    <b-button v-bind:disabled="this.currentNum<=9 || answered==false" @click="submit" >Submit</b-button>
    <b-button v-on:click="next" v-bind:disabled="this.currentNum==10 || !answered" >Next</b-button>
  </b-jumbotron>
  <div id="result">
     <p class="score">You scored {{this.count}} out of 10 !! </p>
     <img v-if="this.count >=0 && this.count<3" src="../assets/images/one.gif">
     <img v-else-if="this.count >=3 && this.count<6" src="../assets/images/two.gif">
     <img v-else-if="this.count >=6 && this.count<8" src="../assets/images/three.gif">
     <img v-else-if="this.count >=8 && this.count>8" src="../assets/images/four.gif">
  </div>
</div>
</template>

<script>
import _ from 'lodash'
export default {
    props: {
        currentQuestion: Object,
        next: Function,
        currentNum: Number
    },
    data(){
       return{
           selectedIndex: null,
           shuffledAns: [],
           count:0,
           correctIndex: null ,
           answered: false
       }
    },
    computed:{
        answers(){
            let answers = [...this.currentQuestion.incorrect_answers];
            answers.push(this.currentQuestion.correct_answer);
            return answers;
        }
    },
    watch:{
       currentQuestion: {
           immediate: true,
           handler(){
             this.selectedIndex = null;
             this.shuffleAns();
             this.answered = false;
           }
       }
    },
    methods: {
        select(index){
            this.selectedIndex = index;
            this.check();
        },
        shuffleAns(){
            let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer];
            this.shuffledAns = _.shuffle(answers);
            this.correctIndex = this.shuffledAns.indexOf(this.currentQuestion.correct_answer);
            return this.shuffledAns;
        },
        check(){
            this.answered = true;
            if(this.selectedIndex=== this.correctIndex){
                this.count++;
            }
            var item = document.querySelector("#item");
            item.className = "list-group disabled";
            console.log(this.count);
        },
        submit(){
            console.log(this.count);
            var jumbo = document.querySelector("#jumbo");
            jumbo.style.display = 'none';
            var result = document.querySelector("#result");
            result.style.display = 'block'
        }
    }
}
</script>

<style scoped>

.list-group{
    margin-bottom: 10% ;
}
.btn{
    margin: 0% 2%;
}
.list-group-item{
    cursor: pointer;
    font-weight: 700;
}
.list-group-item:hover {
    background-color: antiquewhite;
}
.correct{
    background-color: limegreen;
}
.incorrect{
    background-color: #f14242;
}
.disabled{
    pointer-events: none;
}
#result{
    display: none;
    position: absolute;
    left: -2%;
    background-color: blanchedalmond;
    padding-top: 6%;
    height: 26vw;
    margin-top: 16%;
    width: 105%;
}
#parent{
    position: relative;
}
#jumbo{
    background-color: darkslategray;
    margin-bottom: 0%;
    padding: 3rem 2rem;
}
.lead {
    color: white;
}
.btn{
    background-color: black !important;
}
.btn:hover{
    background-color: coral !important;
    border: 1px solid black;
}
.score{
    margin-top: 0;
    margin-bottom: 0.5rem;
    font-size: 1.4rem;
    font-weight: 600;
}
img{
    width: 43%;
}
@media (max-width:1200px){
#result {
  left: -6%;
  height: 32vw;
  width: 116%;
}
}
@media (max-width:992px){
    #result {
        left: -17%;
        height: 39vw;
        width: 136%;
        margin-top: 24%;   
    }
    #parent {
    position: relative;
    width: 125%;
    left: -11%;
    margin-top: 3%;
}
}
@media (max-width:768px){
#parent {
    position: relative;
    width: 150%;
    left: -25%;
    margin-top: 4%;
}
#result {
    height: 46vw;
}
}
@media (max-width:640px){
#parent{
    position: relative;
    width: 116%;
    left: -25%;
    margin-top: 2%;
}
#result{
    left: -5%;
    height: 56vw;
    width: 108%;
}
.lead {
    font-size: 1.1rem;
}
}
@media (max-width:480px){
.lead{
    font-size: 1rem;
}
#parent {
    position: relative;
    width: 131%;
    left: -34%;
    margin-top: 13%;
}
#jumbo {
    padding: 2rem 1rem;
}
#result{
    left: 0%;
    height: 65vw;
    width: 101%;
}
img {
    width: 55%;
}
}
@media (max-width:360px){
img{
    width: 55%;
}
}
</style>
