<template>
  <div id="clock" v-bind:class="themeColor">
    <div id="settings-toggle" @click="toggleSettings">
      <svg fill="white" viewBox="0 0 20 20">
        <path
          d="M5 4a1 1 0 00-2 0v7.268a2 2 0 000 3.464V16a1 1 0 102 0v-1.268a2 2 0 000-3.464V4zM11 4a1 1 0 10-2 0v1.268a2 2 0 000 3.464V16a1 1 0 102 0V8.732a2 2 0 000-3.464V4zM16 3a1 1 0 011 1v7.268a2 2 0 010 3.464V16a1 1 0 11-2 0v-1.268a2 2 0 010-3.464V4a1 1 0 011-1z"
        ></path>
      </svg>
    </div>
    <div id="time-remaining">
      <p id="minutes-remaining">
        {{ Math.floor(timeRemaining / 60) }} :
        {{ Math.floor(timeRemaining % 60) }}
      </p>
    </div>
    <div id="clock-start-toggle" @click="countDown">
      <svg id="start-btn" fill="currentColor" viewBox="0 0 20 20">
        <path
          fill-rule="evenodd"
          d="M10 18a8 8 0 100-16 8 8 0 000 16zM9.555 7.168A1 1 0 008 8v4a1 1 0 001.555.832l3-2a1 1 0 000-1.664l-3-2z"
          clip-rule="evenodd"
        ></path>
      </svg>
      <svg class="hidden" id="stop-btn" fill="currentColor" viewBox="0 0 20 20">
        <path
          fill-rule="evenodd"
          d="M10 18a8 8 0 100-16 8 8 0 000 16zM8 7a1 1 0 00-1 1v4a1 1 0 001 1h4a1 1 0 001-1V8a1 1 0 00-1-1H8z"
          clip-rule="evenodd"
        ></path>
      </svg>
    </div>
    <button id="reset-btn" @click="resetTimer">Reset Timer</button>
    <p id="task-header">Task</p>
    <input type="text" id="task-name" placeholder="What are you working on?" />
  </div>
</template>

<script>
export default {
  props: ["workTime", "shortBreakTime", "longBreakTime", "themeColor"],
  data() {
    return {
      paused: true,
      timeRemaining: this.workTime * 60,
    };
  },

  methods: {
    toggleSettings() {
      clock.style.display = "none";
      settings.style.display = "grid";
    },
    resetTimer() {
      if (this.paused === false) {
        this.paused = true;
        startBtn.classList.toggle("hidden");
        stopBtn.classList.toggle("hidden");
        console.log(this.paused);
      }

      this.timeRemaining = this.workTime * 60;
    },
    countDown() {
      let stopBtn = document.getElementById("stop-btn");
      let startBtn = document.getElementById("start-btn");
      let countInterval = setInterval(() => {
        if (this.paused === false && this.timeRemaining > 0) {
          this.timeRemaining -= 1;
        } else if (this.timeRemaining === 0) {
          this.paused = true;
          startBtn.classList.toggle("hidden");
          stopBtn.classList.toggle("hidden");
          console.log(this.paused);
          alert("Time is Up");
          this.timeRemaining = this.workTime * 60;
        } else {
          clearInterval(countInterval);
        }
      }, 1000);
      if (this.paused === true && this.timeRemaining > 0) {
        this.paused = false;
        startBtn.classList.toggle("hidden");
        stopBtn.classList.toggle("hidden");
        console.log(this.paused);
      } else {
        this.paused = true;
        startBtn.classList.toggle("hidden");
        stopBtn.classList.toggle("hidden");
        console.log(this.paused);
      }
    },
  },
};
</script>

<style>
#task-header {
  width: 100%;
  grid-row: 4;
  grid-column: 1 / 4;
  font-size: 16px;
}

#clock {
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 5fr 1fr 1fr;
  height: 100vh;
  align-items: center;
  justify-items: center;
  color: white;
  display: grid;
  width: 100vw;
}

#settings-toggle {
  grid-column: 1;
  width: 45px;
  align-self: center;
  justify-self: flex-start;
  margin-left: 50px;
}
#task-name {
  grid-row: 5;
  grid-column: 1 / 4;
  align-self: flex-start;
}
input[type="text"] {
  background: none;
  border: none;
  color: white;
  text-align: center;
  font-size: 18px;
}
input[type="text"]::placeholder {
  color: white;
}
#clock-start-toggle {
  width: 75vw;
  height: 75vw;
  max-width: 400px;
  max-height: 400px;
  border: 15px solid white;
  border-radius: 100%;
  grid-row: 3;
  grid-column: 1 / 4;
  transition: all 0.2s ease-in-out;
  background-image: url('<svg fill="white" viewBox="0 0 20 20"><path d="M5 4a1 1 0 00-2 0v7.268a2 2 0 000 3.464V16a1 1 0 102 0v-1.268a2 2 0 000-3.464V4zM11 4a1 1 0 10-2 0v1.268a2 2 0 000 3.464V16a1 1 0 102 0V8.732a2 2 0 000-3.464V4zM16 3a1 1 0 011 1v7.268a2 2 0 010 3.464V16a1 1 0 11-2 0v-1.268a2 2 0 010-3.464V4a1 1 0 011-1z"></path></svg>');
}

#clock-start-toggle:hover {
  opacity: 0.5;
}

@media screen and (max-width: 700px) {
  #settings-toggle {
    grid-row: 1;
    align-self: flex-start;
    margin-top: 15px;
    justify-self: flex-start;
    margin-left: 15px;
  }

  #reset-btn {
    align-self: flex-start;
    margin-top: 15px;
  }
}
</style>
