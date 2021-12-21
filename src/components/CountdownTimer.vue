<template>
  <div class="countdown-timer">
    <h1>{{ msg }}</h1>
    <svg viewBox="0 0 100 100">
      <g class="base-timer-circle">
        <circle class="base-timer-path-elapsed" cx="50" cy="50" r="45" />
      </g>
    </svg>
    <span>
      <h1>{{ formatTime(remainingSeconds) }}</h1>
    </span>
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
      if (durationInMinutes > 0) {
        this.remainingSeconds = durationInMinutes * 60;

        const that = this;
        this.intervalID = setInterval(function () {
          if (that.remainingSeconds === 0) {
            that.stopTimer();
            return;
          }
          that.remainingSeconds -= 1;
        }, 1000);
      }
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

.countdown-timer {
  position: inline;
  height: 300px;
  width: 300px;
}

.base-timer-circle {
  fill: none;
  stroke: none;
}

.base-timer-path-elapsed {
  stroke-width: 7px;
  stroke: grey;
}
</style>
