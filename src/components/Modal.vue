<template>
  <div class="backdrop" @click.self="hideModal">
    <div class="modal">
      <h2>You got the Jordle in {{ guessCounter }} {{ (guessCounter === 1) ? 'attempt' : 'attempts' }}.</h2>
      <p>{{ rank }}</p>
      <p>Refresh the page to try again!</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ['guessCounter'],
  data() {
    return {
      rank: null
    }
  },
  mounted() {
    switch(this.guessCounter){
      case 1:
        this.rank = 'Be honest. Did you cheat?'
      break;
      case 2:
        this.rank = 'Luck has smiled upon you this day.'
      break;
      case 3:
        this.rank = 'Excellent work, my friend.'
      break;
      case 4:
        this.rank = 'Good effort.'
      break;
      case 5:
        this.rank = "We've all been there."
      break;
      default:
        this.rank = 'Wipeout.'
    }
  },
  methods: {
    hideModal() {
      this.$emit('close');
      this.$emit('reset');
    }
  }
}
</script>

<style>
  .modal {
    width: 400px;
    padding: 20px;
    margin: 100px auto;
    background: #9E788F;
    border-radius: 8px;
  }
  .backdrop {
    top: 0;
    position: fixed;
    background: #6c9a8b9f;
    width: 100%;
    height: 100%;
  }
  p {
    font-size: 20px;
  }

</style>
