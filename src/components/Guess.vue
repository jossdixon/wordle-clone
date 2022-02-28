<template>

  <div class="container mb-3">
    <form @keyup.enter="handleSubmit">
    <input
      type="text"
      maxlength="1"
      v-model="first.entry"
      :class="{ present: first.present, placed: first.placed }"
      :disabled="this.formCounter !== this.guessCounter"
    >
    <input
      type="text"
      maxlength="1"
      v-model="second.entry"
      :class="{ present: second.present, placed: second.placed }"
      :disabled="this.formCounter !== this.guessCounter"
    >
    <input
      type="text"
      maxlength="1"
      v-model="third.entry"
      :class="{ present: third.present, placed: third.placed }"
      :disabled="this.formCounter !== this.guessCounter"
    >
    <input
      type="text"
      maxlength="1"
      v-model="fourth.entry"
      :class="{ present: fourth.present, placed: fourth.placed }"
      :disabled="this.formCounter !== this.guessCounter"
    >
    <input
      type="text"
      maxlength="1"
      v-model="fifth.entry"
      :class="{ present: fifth.present, placed: fifth.placed }"
      :disabled="this.formCounter !== this.guessCounter"
    >
    <!-- <input type="submit" v-on:keyup.enter > -->
    <div v-if="entryError" class="error">{{ entryError }}</div>
    <!-- <div v-if="guessResponse" class="error">{{ guessResponse }}</div> -->
    </form>
  </div>

</template>

<script>

export default {
  props: ['word', 'formCounter', 'guessCounter'],
  data() {
    return {
      first: {
        entry: '',
        present: false,
        placed: false
      },
      second: {
        entry: '',
        present: false,
        placed: false
      },
      third: {
        entry: '',
        present: false,
        placed: false
      },
      fourth: {
        entry: '',
        present: false,
        placed: false
      },
      fifth: {
        entry: '',
        present: false,
        placed: false
      },
      entryError: '',
      guessResponse: ''
    }
  },
  methods: {
    handleSubmit() {
      this.guessResponse = '';
      const guessJoined = [this.first.entry, this.second.entry, this.third.entry, this.fourth.entry, this.fifth.entry];
      this.entryError = guessJoined.includes('') ? 'Word is too short' : '';

      if (!this.entryError) {
        while (this.guessResponse === '') {
          console.log(this.word.join(''));
          console.log(guessJoined.join(''));
          if (guessJoined.join('') === this.word.join('')) {
            this.guessResponse = 'Spot on';
            [this.first, this.second, this.third, this.fourth, this.fifth].forEach(i => i.placed = true);
          } else {
            this.word.forEach((letter) => {
              switch(letter) {
                case this.first.entry:
                  if (this.word[0] === letter) {
                    this.guessResponse = 'firstplaced';
                    this.first.placed = true;
                  } else {
                    this.guessResponse = 'firstpresent';
                    this.first.present = true;
                  }
                  break;
                case this.second.entry:
                  if (this.word[1] === letter) {
                    this.guessResponse = 'secondplaced';
                    this.second.placed = true;
                  } else {
                    this.guessResponse = 'secondpresent';
                    this.second.present = true;
                  }
                  break;
                case this.third.entry:
                  if (this.word[2] === letter) {
                    this.guessResponse = 'thirdplaced';
                    this.third.placed = true;
                  } else {
                    this.guessResponse = 'thirdpresent';
                    this.third.present = true;
                  }
                  break;
                case this.fourth.entry:
                  if (this.word[3] === letter) {
                    this.guessResponse = 'fourthplaced';
                    this.fourth.placed = true;
                  } else {
                    this.guessResponse = 'fourthpresent';
                    this.fourth.present = true;
                  }
                  break;
                case this.fifth.entry:
                  if (this.word[4] === letter) {
                    this.guessResponse = 'fifthplaced';
                    this.fifth.placed = true;
                  } else {
                    this.guessResponse = 'fifthpresent';
                    this.fifth.present = true;
                  }
                  break;
                default:
                  console.log('default');
                  this.guessResponse = 'default';
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
    /* border-bottom: 4px solid rgb(107, 106, 106); */
    background-color: whitesmoke;
    box-sizing: border-box;
    text-align: center;
    outline: none;
    font-size: 24px;
    font-weight: bold;
  }
  input[type=text]:focus {
    background-color: lightpink;
  }
  input[type=text].present {
    background-color: goldenrod;
  }
  input[type=text].placed {
    background-color:  seagreen;
  }

</style>
