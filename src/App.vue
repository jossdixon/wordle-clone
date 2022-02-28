<template>
  <h1><strong>DORDLE</strong></h1>
  <div v-for="n in 6" :key="n">
    <Guess :word="word" @emitGuessCounter="increaseCounter" @emitVictory="toggleModal" :formCounter="n" :guessCounter="guessCounter"/>
  </div>
  <div v-if="showModal">
    <Modal @close="toggleModal" :guessCounter="guessCounter">
    </Modal>
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
      guessCounter: 0,
      showModal: false
    }
  },
  methods: {
    increaseCounter() {
      this.guessCounter ++;
    },
    toggleModal() {
      this.showModal = !this.showModal;
    }
  },
  mounted() {
    function sample(array) {
      return array[Math.floor ( Math.random() * array.length )]
    }
    const words = ['words'];
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
  color: darkslategrey;
  padding: 24px;
  background-color: lightblue;

}
h1 {
  display: inline-block;
}
</style>
