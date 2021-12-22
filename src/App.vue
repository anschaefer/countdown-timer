<template>
<CountdownTimer msg="Meeting starts in:"/>
</template>

<script>
import CountdownTimer from './components/CountdownTimer.vue'

export default {
  name: 'App',
  components: {
    CountdownTimer
  }
}
</script>

<style>

html { 
  background: no-repeat center center fixed; 
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
