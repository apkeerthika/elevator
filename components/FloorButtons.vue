<template lang="pug">
.floor-button
  .floor(v-for="(f, i) in floors")
    //- span {{ i }}
    //- button(@click="select(i)") up
    //- button down
    span(:class="{highlighted: current == i}") {{ i }}
    a.btn(@click="select(i)") up
    a.btn down

</template>

<script>
export default {
  props: {
    floors: Number,
    current: Number
  },
  data () {
    return {

    }
  },
  methods: {
    select (i) {
      this.$emit('selected',i)
    }
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
    margin: 2rem
    span
      padding: 0.5rem
      &.highlighted
        border: 1px solid red


    a.btn
      margin-left: 1rem
      border: 1px solid #000
      padding: 1rem
      cursor: pointer
</style>