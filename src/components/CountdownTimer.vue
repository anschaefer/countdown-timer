<template>
  <div class="CountdownTimer">
    <h1>{{ msg }}</h1>
    <h1>{{ formatTime(remainingSeconds) }}</h1>
  </div>
  <div v-if="!intervalID">
    <input v-model="timeoutInMinutes" placeholder="Timeout in minutes" />
    <button class="controlButton" v-on:click="startTimer(timeoutInMinutes)">
      Start Timer
    </button>
  </div>
  <button class="controlButton" v-else v-on:click="stopTimer()">
    Stop Timer
  </button>
</template>

<script>
export default {
  name: "CountdownTimer",
  props: {
    msg: String,
  },
  data() {
    return {
      intervalID: null,
      timeout: null,
      remainingSeconds: 0,
    };
  },
  methods: {
    startTimer(durationInMinutes) {
      this.remainingSeconds = durationInMinutes * 60;

      const that = this;
      this.intervalID = setInterval(function () {
        if (that.remainingSeconds === 0) {
          that.stopTimer();
          return;
        }
        that.remainingSeconds -= 1;
      }, 1000);
    },
    stopTimer() {
      clearInterval(this.intervalID);
      this.remainingSeconds = 0;
      this.intervalID = null;
    },
    formatTime(time) {
      const minutes = Math.floor(time / 60);
      let seconds = time % 60;

      if (seconds < 10) {
        seconds = "0" + seconds;
      }

      return minutes + ":" + seconds;
    },
  },
};
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
.controlButton {
  margin: 40px 0 0;
}
</style>
