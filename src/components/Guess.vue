<template>

  <div class="container mb-3">
    <form @submit.prevent="handleSubmit">
    <input type="text" maxlength="1" v-model="first" :disabled="isCurrent">
    <input type="text" maxlength="1" v-model="second" :disabled="isCurrent">
    <input type="text" maxlength="1" v-model="third" :disabled="isCurrent">
    <input type="text" maxlength="1" v-model="fourth" :disabled="isCurrent">
    <input type="text" maxlength="1" v-model="fifth" :disabled="isCurrent">
    <input type="submit">
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
      isCurrent: false,
      first: '',
      second: '',
      third: '',
      fourth: '',
      fifth: '',
      entryError: '',
      guessResponse: '',
    }
  },
  methods: {
    handleSubmit() {
      this.guessResponse = '';
      const guessJoined = [this.first, this.second, this.third, this.fourth, this.fifth];
      this.entryError = guessJoined.includes('') ? 'Word is too short' : '';

      if (!this.entryError) {
        while (this.guessResponse === '') {
          console.log(this.word);
          console.log(guessJoined);
          // if (this.guessJoined.join() === this.word.join()) {
          //   return this.guessResponse = 'Spot on!'
          // }
          this.word.forEach((letter) => {
            if (guessJoined.includes(letter)) {
              return this.guessResponse = 'Good guess!'
            } else {
              return this.guessResponse = 'Try again'
            }
          })
        }
      }
      this.$emit('emitGuessCounter');
      console.log(this.isCurrent);
      this.isCurrent = (this.formCounter + 1) === this.guessCounter;
    }
  }
}

</script>

<style>
  input[type=text] {
    width: 8%;
    padding: 8px;
    margin: 8px;
    border: none;
    border-bottom: 4px solid darkgray;
    box-sizing: border-box;
    text-align: center;
    outline: none;
    font-size: 24px;
  }
  input[type=text]:focus {
    border-bottom: 4px solid rgb(65, 65, 65)
  }
</style>
