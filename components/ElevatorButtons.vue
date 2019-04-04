<template lang="pug">
.elevator-buttons
  a.btn(:class="{highlighted: currentFloor == i}", v-for="(f, i) in floors") {{ i }}
</template>

<script>
export default {
  props: {
    floors: Number
  },
  data () {
    return {
      currentFloor: 0
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


.btn
  margin: 0.2rem
  padding: 0.5rem 1rem
  display: inline-block
  border: 1px solid #f4f5f7
  &.highlighted
    border: 1px solid red

</style>