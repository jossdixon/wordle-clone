<template>
  <h1><strong>JORDLE</strong></h1>
  <h2 id="orange">Right letter, wrong place.</h2>
  <h2 id="green">Right letter, right place!</h2>
  <div v-for="n in 6" :key="n">
    <Guess
      :word="word"
      @emitGuessCounter="increaseCounter"
      @emitVictory="toggleModal"
      :formCounter="n"
      :guessCounter="guessCounter"
    />
  </div>
  <div v-if="showModal">
    <Modal
      @close="toggleModal"
      :guessCounter="guessCounter"
      @reset="resetGame"
    />
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
    },
    resetGame() {
      this.guessCounter = 9;
    }
  },
  mounted() {
    function sample(array) {
      return array[Math.floor ( Math.random() * array.length )]
    }
    const words = [
      'words',
      'flame',
      'beans',
      'grand',
      'shave',
      'mouth',
      'plane',
      'cabin',
      'doubt',
      'ample',
      'extra',
      'large',
      'query',
      'track'
      ];
    this.word = sample(words).split('');
  }
}
</script>

<style>
#app {
  font-family: 'Fredoka', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #474954;
  padding: 0;
  background-color: #9E788F;
  min-height: 100vh;
  min-width: 100vw;
  margin: 0;
  position: fixed;
  top: 0;
  left: 0;
}
#orange {
  color: #FF7D00;
  text-shadow: 2px 2px 4px #474954;
  letter-spacing: 2px;
}
#green {
  color: #6C9A8B;
  letter-spacing: 2px;
  text-shadow: 2px 2px 4px #474954;
}
h1 {
  font-size: 48px;
}
</style>
