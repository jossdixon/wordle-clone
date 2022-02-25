<template>
  <h1>Wordle Clone</h1>
  <div v-for="n in 6" :key="n">
    <Guess :word="word" @emitGuessCounter="increaseCounter" :formCounter="n" :guessCounter="guessCounter"/>
  </div>
</template>

<script>
import Guess from './components/Guess.vue'

export default {
  name: 'App',
  components: { Guess },
  data() {
    return {
      word: [''],
      guessCounter: 1
    }
  },
  methods: {
    increaseCounter() {
      this.guessCounter ++;
    }
  },
  mounted() {
    function sample(array) {
      return array[Math.floor ( Math.random() * array.length )]
    }
    const words = ['words', 'flame', 'brown'];
    this.word = sample(words).split('');
    console.log(this.word);
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
  padding: 24px;
  background-color:antiquewhite;
  height: 100vh;
}
</style>
