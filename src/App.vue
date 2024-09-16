<template>
  <div class="container">
    <img :src="timerImage" alt="Countdown Timer Image" class="timer-image" />
    <h1>Countdown Timer</h1>
    
    <div>
      <input
        type="number"
        v-model="days"
        min="0"
        placeholder="Days"
      />
      <input
        type="number"
        v-model="hours"
        min="0"
        placeholder="Hours"
      />
      <input
        type="number"
        v-model="timeInput"
        min="1"
        max="60"
        placeholder="Seconds"
      />
    </div>

    <button @click="startCountdown">Start Countdown</button>
    <p>Time Left: {{ formatTime(timeLeft) }}</p>
  </div>
</template>

<script>
import timerImage from '/project3/assets/STC-Primary.png';

export default {
  data() {
    return {
      days: null,
      hours: null,
      timeInput: null,
      timeLeft: 0,
      timer: null,
      timerImage,
    };
  },
  methods: {
    startCountdown() {
      this.timeLeft = (this.days || 0) * 86400 + (this.hours || 0) * 3600 + (this.timeInput || 0);

      if (this.timer) {
        clearInterval(this.timer);
      }

      this.timer = setInterval(() => {
        if (this.timeLeft > 0) {
          this.timeLeft--;
        } else {
          clearInterval(this.timer);
          this.timer = null;
        }
      }, 1000);
    },
    formatTime(seconds) {
      const days = Math.floor(seconds / 86400);
      const hours = Math.floor((seconds % 86400) / 3600);
      const minutes = Math.floor((seconds % 3600) / 60);
      const secs = seconds % 60;
      return `${days}d ${hours}h ${minutes}m ${secs}s`;
    },
  },
};
</script>

<style>
@import '../src/styles.css';
</style>
