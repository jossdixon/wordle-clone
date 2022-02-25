<template>
  <h1>Wordle Clone</h1>
  <Guess :word="word" @emitGuessCounter="increaseCounter" :formCounter="1" :guessCounter="guessCounter"/>
  <Guess :word="word" @emitGuessCounter="increaseCounter" :formCounter="2" :guessCounter="guessCounter"/>
  <Guess :word="word" @emitGuessCounter="increaseCounter" :formCounter="3" :guessCounter="guessCounter"/>
  <Guess :word="word" @emitGuessCounter="increaseCounter" :formCounter="4" :guessCounter="guessCounter"/>
  <Guess :word="word" @emitGuessCounter="increaseCounter" :formCounter="5" :guessCounter="guessCounter"/>
  <Guess :word="word" @emitGuessCounter="increaseCounter" :formCounter="6" :guessCounter="guessCounter"/>
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
      console.log(`App says guess count is ${this.guessCounter}`);
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
  margin-top: 60px;
}
</style>
