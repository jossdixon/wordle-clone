<template>
  <form>
    <input type="text" v-model="first">
    <input type="text" v-model="second">
    <input type="text" v-model="third">
    <input type="text" v-model="fourth">
    <input type="text" v-model="fifth">
  </form>
</template>

<script>
export default {
  data() {
    return {
      first: '',
      second: '',
      third: '',
      fourth: '',
      fifth: ''
    }
  },
  methods: {
    handleSubmit() {
      const wordJoined = [this.first, this.second, this.third, this.fourth, this.fifth]
      this.entryError = wordJoined.length > 5 ? '' : 'Word is too short'

      if (!this.entryError) {
        console.log(wordJoined)
      }
    }
  }
}

</script>
