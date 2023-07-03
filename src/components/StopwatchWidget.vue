<template>
  <div class="stopwatch-widget">
    <h2>Stopwatch Widget</h2>
    <div class="time">{{ formatTime }}</div>
    <div class="controls">
      <button @click="startStopwatch" :disabled="isRunning">Start</button>
      <button @click="stopStopwatch" :disabled="!isRunning">Stop</button>
      <button @click="resetStopwatch">Reset</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'StopwatchWidget',
  data() {
    return {
      isRunning: false,
      startTime: null,
      currentTime: null,
      elapsedTime: 0
    };
  },
  computed: {
    formatTime() {
      const minutes = Math.floor(this.elapsedTime / 60000);
      const seconds = Math.floor((this.elapsedTime % 60000) / 1000);
      const milliseconds = Math.floor((this.elapsedTime % 1000) / 10);
      return `${padTime(minutes)}:${padTime(seconds)}:${padTime(milliseconds)}`;
    }
  },
  methods: {
    startStopwatch() {
      if (!this.isRunning) {
        this.isRunning = true;
        this.startTime = Date.now() - this.elapsedTime;
        this.updateTime();
      }
    },
    stopStopwatch() {
      if (this.isRunning) {
        this.isRunning = false;
        this.elapsedTime = Date.now() - this.startTime;
      }
    },
    resetStopwatch() {
      this.isRunning = false;
      this.startTime = null;
      this.currentTime = null;
      this.elapsedTime = 0;
    },
    updateTime() {
      if (this.isRunning) {
        this.currentTime = Date.now();
        this.elapsedTime = this.currentTime - this.startTime;
        requestAnimationFrame(this.updateTime);
      }
    }
  }
};

function padTime(value) {
  return value.toString().padStart(2, '0');
}
</script>

<style scoped>
.stopwatch-widget {
  border: 1px solid #ccc;
  padding: 20px;
  margin-bottom: 20px;
  text-align: center;
}

.time {
  font-size: 2em;
  margin-bottom: 10px;
}

.controls {
  display: flex;
  justify-content: center;
}

.controls button {
  margin-right: 10px;
  font-size: 1em;
  padding: 5px 10px;
  background-color: #000000;
  border: none;
  cursor: pointer;
}

.controls button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.controls button:hover {
  background-color: #aaa;
}
</style>
