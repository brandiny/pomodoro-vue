<template>
  <h1>Tomato Timer</h1>

  <!-- displays the clock ticking down -->
  <Timer @stop="pauseTimer" :status="status" :running="runTimer">
    <template v-slot:minutes>{{minutes}}</template>
    <template v-slot:seconds>{{seconds}}</template>
  </Timer>

  <!-- displays the status of either work/break and buttons -->
  <Status @break="setTimerBreak" @work="setTimerWork" :status="status"/>

</template>

<script>

import Timer from "./components/Timer.vue"
import Status from "./components/Status.vue"

export default {
  name: 'App',
  components: { Timer, Status },
  data() {
    return {
      runTimer: true,
      minutes: "0",
      seconds: "03",
      status: "work",
      lastStatus: null,
      WORK_MINUTES: 25,
      BREAK_MINUTES: 5
    }
  },

  methods: {
    pauseTimer() {
      this.runTimer = !this.runTimer
    },

    updateTime() {
        let m = parseInt(this.minutes);
        let s = parseInt(this.seconds) - 1;

        if (m == 0 && s == 0) {
            if (this.status == "work") {this.setTimerBreak()}
            else if (this.status == "break") {this.setTimerWork()}
            return
        }

        if (s == -1) {
          this.seconds = (s + 60).toString();
          this.minutes = (m - 1).toString();
        } 

        else if (s % 10 == s) {
          this.seconds = "0" + s.toString();
        } 
        
        else {
          this.seconds = s.toString();
          this.minutes = m.toString();
        }
    },

    setTimerBreak() {
      this.status = "break"
      this.minutes = this.BREAK_MINUTES.toString()
      this.seconds = "00";
    },

    setTimerWork() {
      this.status = "work"
      this.minutes = this.WORK_MINUTES.toString()
      this.seconds = "00";
    }
  },
 
  
  mounted() {
    setInterval(() => {
      if (this.runTimer) {
        this.updateTime()
      }
    }, 1000)
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
