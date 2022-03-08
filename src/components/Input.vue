<template>
  <input
    type="text"
    maxlength="1"
    v-model="this.letter"
    :class="{ present: first.present, placed: first.placed }"
    :disabled="(this.formCounter - 1) !== this.guessCounter"
    v-on:keyup="$event.target.nextElementSibling.focus()"
  >
</template>

<script>
  export default {
    name: 'Input',
    props: ['inputCounter'],
    data() {
      return {
        letter: ''
      }
    },
    methods: {
      handleKeyup() {

      }
    }
  }


</script>

<style>

</style>
