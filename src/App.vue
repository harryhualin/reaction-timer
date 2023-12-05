
import { ReactiveEffect } from 'vue';
<template>
  <h1>Ninja Reaction Timer</h1>
  <button @click="start" :disabled="isPlaying">play</button>
  <Block v-if="isPlaying" :delay="delay" @end="endGame"/>
  <!-- <p v-if="showResults">Reaction time:{{score}}</p> -->
  <Results v-if="showResults" :score="score"></Results>
</template>

<script>
import Block from './components/Block.vue'
import Results from './components/Results.vue'

export default {
  name: 'App',
  components: {
    Block,
    Results
  },
  data(){
    return {
      isPlaying:false,
      delay:null,
      score:null,
      showResults:false
    }
  },
  methods:{
    start(){
      this.isPlaying=true
      this.delay=2000+Math.random()*5000
      //console.log(this.delay)
      this.showResults=false
    },
    endGame(reactionTime){
        this.score=reactionTime
        this.isPlaying=false
        this.showResults=true
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}
button {
  background: #0faf87;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
}
button[disabled] {
  opacity: 0.2;
  cursor: not-allowed;
}
</style>
