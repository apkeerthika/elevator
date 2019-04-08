<template lang="pug">
.page
  elevator-buttons(:floors="floors", :current="current", @selected="addRequests")
  br/
  br/
  floor-buttons(:floors="floors", :current="current",@selected="act")
  br/
  br/
  h2
    | Next Floor:&nbsp;&nbsp;
    span {{ next }}
  h2
    | Current Floor:&nbsp;&nbsp;
    span {{ current }}
  h2
    | Selected request:&nbsp;&nbsp;
    span.up {{ requests.toString() }}
  h2
    | Selected up:&nbsp;&nbsp;
    span {{ acts.toString() }}

  input(type="number", v-model="fullfill")
  button(@click="done(fullfill)") Do {{ fullfill }}
  h2
    | Delete Finished level:&nbsp;&nbsp;
    span {{ fullfill }}
</template>


<script>
import _ from 'lodash'
import ElevatorButtons from '~/components/ElevatorButtons'
import FloorButtons from '~/components/FloorButtons'

const sleep = ms => new Promise(res => setTimeout(res, ms));

export default {
  data () {
    return {
      floors: 5,
      current: 0,
      fullfill: 0,
      // next: 0,
      requests: [],
      acts: [],
      direction: 1
    }
  },
  computed: {
    next () {
      if (this.direction == 1) {
        console.log(this.direction)
        return _(this.requests)
                .filter(request => this.current < this.floors)
                .min()
      } else if (this.direction == -1) {
        console.log(this.direction)
        return _(this.requests)
                .filter(request => this.current > this.floors)
                .max()
      } else {
        console.log(this.done())
        this.done()
      }
    }
  },
  methods: {
    move (i) {
      this.current = i
    },
    addRequests (i) {
      // console.log(i)
      // this.next = i
      this.requests.push(i)
    },
    act (i) {
      // console.log(i)
      // this.next = i
      this.acts.push(i)
    },
    done (f) {
      // console.log(f)
      const removedItem = _.remove(this.requests, f)
      return removedItem
      // this.$delete(this.requests, f)
    }
  },
  watch: {
    async next () {
      if (this.current < this.next) {
        console.log('labsk', this.current, this.next)
        for(let i=this.current; i<=this.next; i++) {
          await sleep(1000)
          this.move(i)
          this.direction = 1
        }
      }
      else if (this.current > this.next) {
        console.log('labsk', this.current, this.next)
        for(let i=this.current; i>=this.next; i--) {
          await sleep(1000)
          this.move(i)
          this.direction = -1
        }
      }
    }
  },
  mounted () {
  },
  components: {
    ElevatorButtons,
    FloorButtons
  }
}
</script>

<style lang="sass" scoped>
.up
  // border: 1px solid #e4e5e7
  // padding: 0.5rem 1.2rem
</style>
