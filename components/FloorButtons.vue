<template lang="pug">
.floor-button
  .floor(v-for="(f, i) in floors")
    span {{ i }}
    button up
    button down
    
</template>

<script>
export default {
  props: {
    floors: Number
  },
  data () {
    return {

    }
  },
  methods: {

  },
  components: {

  }
}
</script>

<style lang="sass" scoped>
// @import 'assets/styles/includes'
.floor-button
  display: flex
  flex-direction: column-reverse
  .floor
    margin: 1rem
    button
      margin-left: 1rem


</style>