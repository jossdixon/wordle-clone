<template>
  <div v-if="showModal">
    <Modal :guessCounter="guessCounter" @close="showModal" />
  </div>
  <h1><strong>DORDLE</strong></h1>
  <div v-for="n in 6" :key="n">
    <Guess :word="word" @emitGuessCounter="increaseCounter" @emitVictory="showVictory" :formCounter="n" :guessCounter="guessCounter"/>
  </div>
</template>

<script>
import Guess from './components/Guess.vue'
import Modal from './components/Modal.vue'

export default {
  name: 'App',
  components: { Guess, Modal },
  data() {
    return {
      word: [''],
      guessCounter: 1,
      showModal: false
    }
  },
  methods: {
    increaseCounter() {
      this.guessCounter ++;
    },
    showVictory() {
      this.showModal = !this.showModal;
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
  font-family: 'Fredoka', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding: 24px;
  background-color: lightblue;
  height: 100vh;
}
</style>
