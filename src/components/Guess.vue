<template>

  <div class="container mb-3">
    <form @keyup.enter="handleSubmit">
    <input
      type="text"
      maxlength="1"
      v-model="first"
      :class="{ present: firstPresent, placed: firstPlaced }"
      :disabled="this.formCounter !== this.guessCounter"
    >
    <input
      type="text"
      maxlength="1"
      v-model="second"
      :class="{ present: secondPresent, placed: secondPlaced }"
      :disabled="this.formCounter !== this.guessCounter"
    >
    <input
      type="text"
      maxlength="1"
      v-model="third"
      :class="{ present: thirdPresent, placed: thirdPlaced }"
      :disabled="this.formCounter !== this.guessCounter"
    >
    <input
      type="text"
      maxlength="1"
      v-model="fourth"
      :class="{ present: fourthPresent, placed: fourthPlaced }"
      :disabled="this.formCounter !== this.guessCounter"
    >
    <input
      type="text"
      maxlength="1"
      v-model="fifth"
      :class="{ present: fifthPresent, placed: fifthPlaced }"
      :disabled="this.formCounter !== this.guessCounter"
    >
    <!-- <input type="submit" v-on:keyup.enter > -->
    <div v-if="entryError" class="error">{{ entryError }}</div>
    <div v-if="guessResponse" class="error">{{ guessResponse }}</div>
    </form>
  </div>

</template>

<script>

export default {
  props: ['word', 'formCounter', 'guessCounter'],
  data() {
    return {
      first: '',
      firstPresent: false,
      firstPlaced: false,
      second: '',
      secondPresent: false,
      secondPlaced: false,
      third: '',
      thirdPresent: false,
      thirdPlaced: false,
      fourth: '',
      fourthPresent: false,
      fourthPlaced: false,
      fifth: '',
      fifthPresent: false,
      fifthPlaced: false,
      entryError: '',
      guessResponse: ''
    }
  },
  methods: {
    handleSubmit() {
      this.guessResponse = '';
      const guessJoined = [this.first, this.second, this.third, this.fourth, this.fifth];
      this.entryError = guessJoined.includes('') ? 'Word is too short' : '';

      if (!this.entryError) {
        while (this.guessResponse === '') {
          console.log(this.word.join(''));
          console.log(guessJoined.join(''));
          if (guessJoined.join('') === this.word.join('')) {
            this.guessResponse = 'Spot on!';
          } else {
            this.word.forEach((letter) => {
              if (guessJoined.includes(letter)) {
              } else {
                return this.guessResponse = 'Try again'
              }
            })
          }
        }
        this.$emit('emitGuessCounter')
      }
    }
  }
}

</script>

<style>
  input[type=text] {
    width: 5%;
    padding: 8px;
    margin: 16px;
    border: none;
    border-bottom: 4px solid rgb(107, 106, 106);
    background-color: whitesmoke;
    box-sizing: border-box;
    text-align: center;
    outline: none;
    font-size: 24px;
  }
  input[type=text]:focus {
    border-bottom: 4px solid rgb(221, 196, 196);
  }
  input[type=text].present {
    border-bottom: 4px solid goldenrod;
  }
  input[type=text].placed {
    border-bottom: 4px solid seagreen;
  }

</style>
