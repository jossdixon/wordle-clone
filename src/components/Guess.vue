<template>

  <div>
    <form @keyup.enter="handleSubmit">
    <input
      type="text"
      maxlength="1"
      v-model="first.entry"
      :class="{ present: first.present, placed: first.placed }"
      :disabled="(this.formCounter - 1) !== this.guessCounter"
      v-on:keyup="$event.target.nextElementSibling.focus()"
    >
    <input
      type="text"
      maxlength="1"
      v-model="second.entry"
      :class="{ present: second.present, placed: second.placed }"
      :disabled="(this.formCounter - 1) !== this.guessCounter"
      v-on:keyup="$event.target.nextElementSibling.focus()"
    >
    <input
      type="text"
      maxlength="1"
      v-model="third.entry"
      :class="{ present: third.present, placed: third.placed }"
      :disabled="(this.formCounter - 1) !== this.guessCounter"
      v-on:keyup="$event.target.nextElementSibling.focus()"
    >
    <input
      type="text"
      maxlength="1"
      v-model="fourth.entry"
      :class="{ present: fourth.present, placed: fourth.placed }"
      :disabled="(this.formCounter - 1) !== this.guessCounter"
      v-on:keyup="$event.target.nextElementSibling.focus()"
    >
    <input
      type="text"
      maxlength="1"
      v-model="fifth.entry"
      :class="{ present: fifth.present, placed: fifth.placed }"
      :disabled="(this.formCounter - 1) !== this.guessCounter"
    >
    </form>
    <div v-if="entryError" class="error">{{ entryError }}</div>
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
      const letters =
      [
        this.first.entry,
        this.second.entry,
        this.third.entry,
        this.fourth.entry,
        this.fifth.entry
      ].map(i => i.toLowerCase());
      this.entryError = letters.includes('') ? 'Word is too short' : '';
      // const regex = /^[A-Za-z]+$/;
      // this.entryError = regex.test(letters.join('')) ? '' : 'Letters only, please.';
      if (!this.entryError) {
        while (this.guessResponse === '') {
          if (letters.join('') === this.word.join('')) {
            this.guessResponse = 'Spot on';
            [this.first, this.second, this.third, this.fourth, this.fifth].forEach(i => i.placed = true);
            this.$emit('emitVictory');
          } else {
            this.word.forEach((letter) => {
              switch(letter) {
                case letters[0]:
                  if (this.word[0] === letter) {
                    this.guessResponse = 'firstplaced';
                    this.first.placed = true;
                  } else {
                    this.guessResponse = 'firstpresent';
                    this.first.present = true;
                  }
                  break;
                case letters[1]:
                  if (this.word[1] === letter) {
                    this.guessResponse = 'secondplaced';
                    this.second.placed = true;
                  } else {
                    this.guessResponse = 'secondpresent';
                    this.second.present = true;
                  }
                  break;
                case letters[2]:
                  if (this.word[2] === letter) {
                    this.guessResponse = 'thirdplaced';
                    this.third.placed = true;
                  } else {
                    this.guessResponse = 'thirdpresent';
                    this.third.present = true;
                  }
                  break;
                case letters[3]:
                  if (this.word[3] === letter) {
                    this.guessResponse = 'fourthplaced';
                    this.fourth.placed = true;
                  } else {
                    this.guessResponse = 'fourthpresent';
                    this.fourth.present = true;
                  }
                  break;
                case letters[4]:
                  if (this.word[4] === letter) {
                    this.guessResponse = 'fifthplaced';
                    this.fifth.placed = true;
                  } else {
                    this.guessResponse = 'fifthpresent';
                    this.fifth.present = true;
                  }
                  break;
                default:
                  this.guessResponse = 'break';
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
  form {
    display: flex;
    align-items: center;
    justify-content: center;
  }
  input[type=text] {
    width: 4rem;
    line-height: 2rem;
    padding: 8px;
    padding-bottom: 12px;
    margin: 8px;
    font-size: 36px;
    box-shadow: 0 0 15px rgba(0,0,0,0.3);
    border: none;
    background-color: #FBFFF1;
    box-sizing: border-box;
    text-align: center;
    outline: none;
    font-family: 'Fredoka', sans-serif;
  }
  input[type=text]:focus {
    background-color: #F3FFD6;
  }
  input[type=text].present {
    background-color: #FF7D00;
  }
  input[type=text].placed {
    background-color: #6C9A8B;
  }

</style>
