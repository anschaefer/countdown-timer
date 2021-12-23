<template>
  <div class="countdown-timer">
    <h1>{{ msg }}</h1>
    <svg viewBox="0 0 100 100">
      <g class="base-timer-circle">
        <circle class="base-timer-path-elapsed" cx="50" cy="50" r="45" />
      </g>
    </svg>
    <span class="base-timer-label">
      {{ formatTime(remainingSeconds) }}
    </span>
  </div>
  <div class="controls">
    <div v-if="!intervalID">
      <input v-model="timeoutInMinutes" placeholder="Timeout in minutes" />
      <button class="controlButton" v-on:click="startTimer(timeoutInMinutes)">
        Start Timer
      </button>
    </div>
    <button class="controlButton" v-else v-on:click="stopTimer()">
      Stop Timer
    </button>
  </div>
  <button class="controlButton" @click="openFileInput">
    Change Background Image
  </button>
  <input
    id="file-input"
    type="file"
    accept="image/*"
    @change="changeBackgroundImage($event)"
  />
</template>

<script>
export default {
  name: "CountdownTimer",
  props: {
    msg: String
  },
  mounted() {},
  data() {
    return {
      intervalID: null,
      timeoutInMinutes: null,
      remainingSeconds: 0
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
    openFileInput() {
      document.getElementById("file-input").click();
    },
    changeBackgroundImage(event) {
      const file = event.target.files[0];
      let reader = new FileReader();
      reader.addEventListener("load", function () {
        const url = reader.result;
        document.documentElement.style.backgroundImage = "url(" + url + ")";
      });
      if (file) {
        reader.readAsDataURL(file);
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  margin: 40px 0 40px 0;
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

.controls {
  margin: 100px 0 0;
}

.controlButton {
  margin: 40px 0 0;
}

.countdown-timer {
  position: inline;
  margin: auto;
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
  animation-name: circleAnimation;
  animation-duration: 4s;
  animation-iteration-count: infinite;
  animation-direction: alternate;
}

.base-timer-label {
  position: absolute;

  /* Size should match the parent container */
  width: 300px;
  height: 300px;

  /* Keep the label aligned to the top */
  top: 140px;

  /* Create a flexible box that centers content vertically and horizontally */
  display: flex;
  align-items: center;
  justify-content: center;

  /* Sort of an arbitrary number; adjust to your liking */
  font-size: 48px;
}

#file-input {
  display: none;
}

@keyframes circleAnimation {
  from {sroke: white;}
  to {stroke: skyblue;}
}


</style>
