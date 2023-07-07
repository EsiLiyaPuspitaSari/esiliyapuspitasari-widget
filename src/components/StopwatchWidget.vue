<template>
  <div class="stopwatch-container">
    <h2 class="header">Penghitung Detik</h2>
    <div class="stopwatch">
      <p>{{ formatTime }}</p>
      <div class="controls">
        <button @click="start" :disabled="isRunning" class="button-primary">Start</button>
        <button @click="stop" :disabled="!isRunning" class="button-secondary">Stop</button>
        <button @click="reset" :disabled="isRunning" class="button-tertiary">Reset</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isRunning: false,
      elapsedTime: 0,
      startTime: null,
    };
  },
  computed: {
    formatTime() {
      const minutes = Math.floor(this.elapsedTime / 60000);
      const seconds = Math.floor((this.elapsedTime % 60000) / 1000);
      const milliseconds = Math.floor((this.elapsedTime % 1000) / 10);

      return `${this.padTime(minutes)}:${this.padTime(seconds)}:${this.padTime(milliseconds)}`;
    },
  },
  methods: {
    padTime(time) {
      return time.toString().padStart(2, '0');
    },
    start() {
      if (!this.isRunning) {
        this.startTime = Date.now() - this.elapsedTime;
        this.isRunning = true;
        this.timer = setInterval(() => {
          this.elapsedTime = Date.now() - this.startTime;
        }, 10);
      }
    },
    stop() {
      if (this.isRunning) {
        clearInterval(this.timer);
        this.isRunning = false;
      }
    },
    reset() {
      this.stop();
      this.elapsedTime = 0;
    },
  },
};
</script>

<style scoped>
.header {
  display: inline-block;
  font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  text-shadow: #070707 1px 1px 2px;
  padding: 4px 9px;
  
  color: rgb(255, 255, 255);
  padding: 12px 12px 12px;
  background-color: #4b454033;
  box-shadow: #000000 1px 1px 5px;
  border-bottom-style: outset;
  border-right-style: ridge;
  border-left-style:outset;
  border-top-style:outset;
  
  animation: headerShadowColorChange 2s infinite;
}



.stopwatch-container {
  background-color: #f0efeb;
  padding-top: 33px;
  padding-bottom: 88px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  animation: containerShadowColorChange 5s infinite;
}

@keyframes containerShadowColorChange {
  0% { box-shadow: 0 0 10px green; }
  20% { box-shadow: 0 0 10px yellow; }
  40% { box-shadow: 0 0 10px orange; }
  60% { box-shadow: 0 0 10px red; }
  80% { box-shadow: 0 0 10px blue; }
  100% { box-shadow: 0 0 10px green; }
}

.stopwatch p {
  font-size: 24px;
  margin: 0;
  color: rgb(0, 0, 0);
}

.stopwatch .controls {
  margin-top: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.stopwatch .controls button {
  padding: 10px 20px;
  margin: 0 9px;
  font-size: 16px;
  border-radius: 4px;
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2)}

.stopwatch .controls button.button-primary {
  background-color: #00fd08fd;
  color: white;
}

.stopwatch .controls button.button-secondary {
  background-color: #ffee00a1;
  color:rgb(19, 13, 13);
}

.stopwatch .controls button.button-tertiary {
  background-color: #fd0000;
  color: white;
}

.stopwatch .controls button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.stopwatch .controls button:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px8px rgba(0, 0, 0, 0.2);
}

.stopwatch .controls button:active {
  transform: translateY(0);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}
</style>
