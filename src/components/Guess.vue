<template>
  <div class="container">
    <form @submit.prevent="handleSubmit">
    <input type="text" v-model="first">
    <input type="text" v-model="second">
    <input type="text" v-model="third">
    <input type="text" v-model="fourth">
    <input type="text" v-model="fifth">
    <input type="submit">
    <div v-if="entryError" class="error">{{ entryError }}</div>
    <div v-if="guessResponse" class="error">{{ guessResponse }}</div>
    </form>
  </div>

</template>

<script>

export default {
  props: ['word'],
  data() {
    return {
      first: '',
      second: '',
      third: '',
      fourth: '',
      fifth: '',
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
    }
  }
}

</script>

<style>
  input[type=text] {
    width: 10%;
    padding: 12px 20px;
    margin: 8px 0;
    box-sizing: border-box;
  }
</style>
