<template lang="pug">
.page
  elevator-buttons(:floors="floors", :current="current", @selected="request")
  br/
  br/
  floor-buttons(:floors="floors", :current="current", @selectedUp="addUpRequest")
  br/
  br/
  h2
    | Next Floor:&nbsp;&nbsp;
    span {{ next }}
  h2
    | Current Floor:&nbsp;&nbsp;
    span {{ current }}
  h2
    | Selected Up:&nbsp;&nbsp;
    span(v-for="(u, i) in up") {{ u }}
</template>


<script>
import ElevatorButtons from '~/components/ElevatorButtons'
import FloorButtons from '~/components/FloorButtons'

const sleep = ms => new Promise(res => setTimeout(res, ms));

export default {
  data () {
    return {
      floors: 5,
      current: 0,
      next: 0,
      up: []
    }
  },
  methods: {
    request (i) {
      this.next = i
    },
    move (i) {
      this.current = i
    },
    addUpRequest (i) {
      console.log(i)
      this.up.push(i, 'up')
    }
  },
  watch: {
    async next () {
      if (this.current < this.next) {
        for(let i=this.current; i<=this.next; i++) {
          await sleep(1000)
          this.move(i)
        }
      }
      else if (this.current > this.next) {
        for(let i=this.current; i>=this.next; i--) {
          await sleep(1000)
          this.move(i)
        }
      }
    }
  },
  components: {
    ElevatorButtons,
    FloorButtons
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
