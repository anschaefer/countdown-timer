<template>
  <div class="CountdownTimer">
    <h1>{{ msg }}</h1>
    <h1>{{ remainingSeconds }}</h1>
  </div>
  <div v-if="!intervalID">
    <input  v-model="timeout" placeholder="Timeout">
    <button v-on:click="startTimer(timeout)">Start Timer</button>
  </div>
  <button v-else v-on:click="stopTimer()">Stop Timer</button>
</template>

<script>
export default {
  name: 'CountdownTimer',
  props: {
    msg: String
  },
  mounted() {
  },
  data() {
    return {
      timeout: null,
      remainingSeconds: 0,
      intervalID: null
    }
  },
  methods: {
    startTimer(durationInMinutes) {
      this.remainingSeconds = durationInMinutes * 60

      const that = this
      this.intervalID = setInterval( function() {
        if(that.remainingSeconds === 0) {
          that.stopTimer()
          return
        }
        that.remainingSeconds -= 1
      }, 1000)
    },
    stopTimer() {
      clearInterval(this.intervalID)
      this.remainingSeconds = 0
      this.intervalID = null
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
