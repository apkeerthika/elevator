<template lang="pug">
.elevator-buttons
  a.btn(:class="{highlighted: current == i}", v-for="(f, i) in floors", @click="select(i)") {{ i }}
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
      this.$emit('selected', i)
    }
  },
  components: {

  }
}
</script>

<style lang="sass" scoped>
// @import 'assets/styles/includes'


.btn
  cursor: pointer
  margin: 0.2rem
  padding: 0.5rem 1rem
  display: inline-block
  border: 1px solid #f4f5f7
  &.highlighted
    border: 1px solid red

</style>