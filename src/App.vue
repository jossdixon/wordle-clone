<template>
  <h1>Wordle Clone</h1>
  <Guess :word="word"/>
</template>

<script>
import Guess from './components/Guess.vue'

export default {
  name: 'App',
  components: { Guess },
  data() {
    return {
      word: [''],
    }
  },
  mounted() {
    function sample(array) {
      return array[Math.floor ( Math.random() * array.length )]
    }
    const words = ['words', 'flame'];
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
