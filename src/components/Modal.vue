<template>
  <div class="backdrop" @click.self="hideModal">
    <div class="modal">
      <div class="text">
        <h2>You got the Dordle in {{ guessCounter }} guesses.</h2>
        <h4>{{ rank }}</h4>
      </div>
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
        this.rank = 'Jammy. Very jammy.'
      break;
      case 3:
        this.rank = 'Solid guessing, my friend.'
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
    }
  }
}
</script>

<style>
  .modal {
    width: 400px;
    padding: 20px;
    margin: 100px auto;
    background: whitesmoke;
    border-radius: 8px;
  }
  .backdrop {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: lightgray;
    opacity: 0.5;
  }

</style>
