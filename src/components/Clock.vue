/* eslint-disable no-unused-vars */
<template>
  <div id="clock" v-bind:class="themeColor">
    <div id="settings-toggle" @click="showSettings">
      <svg
        viewBox="0 0 16 16"
        class="bi bi-gear-fill"
        fill="currentColor"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          fill-rule="evenodd"
          d="M9.405 1.05c-.413-1.4-2.397-1.4-2.81 0l-.1.34a1.464 1.464 0 0 1-2.105.872l-.31-.17c-1.283-.698-2.686.705-1.987 1.987l.169.311c.446.82.023 1.841-.872 2.105l-.34.1c-1.4.413-1.4 2.397 0 2.81l.34.1a1.464 1.464 0 0 1 .872 2.105l-.17.31c-.698 1.283.705 2.686 1.987 1.987l.311-.169a1.464 1.464 0 0 1 2.105.872l.1.34c.413 1.4 2.397 1.4 2.81 0l.1-.34a1.464 1.464 0 0 1 2.105-.872l.31.17c1.283.698 2.686-.705 1.987-1.987l-.169-.311a1.464 1.464 0 0 1 .872-2.105l.34-.1c1.4-.413 1.4-2.397 0-2.81l-.34-.1a1.464 1.464 0 0 1-.872-2.105l.17-.31c.698-1.283-.705-2.686-1.987-1.987l-.311.169a1.464 1.464 0 0 1-2.105-.872l-.1-.34zM8 10.93a2.929 2.929 0 1 0 0-5.86 2.929 2.929 0 0 0 0 5.858z"
        />
      </svg>
    </div>
    <div id="time-remaining">
      <p id="minutes-remaining">
        {{ minutesRemaining }} :
        {{ secondsRemaining }}
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
    <p id="reset-btn" @click="resetTimer">Reset</p>
    <p id="task-header">Task</p>
    <input type="text" id="task-name" placeholder="What are you working on?" />
  </div>
</template>

<script>
export default {
  props: [
    "workTime",
    "breakTime",
    "themeColor",
    "paused",
    "mode",
    "timeRemaining",
  ],
  computed: {
    minutesRemaining: function() {
      //console.log(this.timeRemaining)
      if (Math.floor(this.timeRemaining / 60) < 10) {
        return "0" + Math.floor(this.timeRemaining / 60);
      } else {
        return Math.floor(this.timeRemaining / 60);
      }
    },
    secondsRemaining: function() {
      if (Math.floor(this.timeRemaining % 60) < 10) {
        return "0" + Math.floor(this.timeRemaining % 60);
      } else {
        return Math.floor(this.timeRemaining % 60);
      }
    },
  },
  methods: {
    showSettings() {
      this.$emit("showSettings", true);
    },
    resetTimer() {
      let stopBtn = document.getElementById("stop-btn");
      let startBtn = document.getElementById("start-btn");
      if (this.paused === false) {
        this.paused = true;
        startBtn.style.display = "block";
        stopBtn.style.display = "none";
        //console.log(this.paused);
      }
      if (this.mode === "work") {
        this.timeRemaining = this.workTime * 60;
      } else if (this.mode === "break") {
        this.timeRemaining = this.breakTime * 60;
      }
    },
    countDown() {
      let stopBtn = document.getElementById("stop-btn");
      let startBtn = document.getElementById("start-btn");
      let countInterval = setInterval(() => {
        if (this.paused === false && this.timeRemaining > 0) {
          this.timeRemaining -= 1;
        } else if (this.timeRemaining === 0) {
          this.paused = true;
          startBtn.style.display = "block";
          stopBtn.style.display = "none";
          //console.log(this.paused);
          if (this.mode === "work") {
            this.mode = "break";
            alert("Entering Break Mode");
            clearInterval(countInterval);
            this.timeRemaining = this.breakTime * 60;
            this.countDown();
          } else if (this.mode === "break") {
            alert("Back To Work!");
            this.mode = "work";
            this.timeRemaining = this.workTime * 60;
            this.countDown();
          } else {
            //console.log("ERROR: INCORRECT MODE");
          }
        } else {
          clearInterval(countInterval);
        }
      }, 1000);
      if (this.paused === true && this.timeRemaining > 0) {
        this.paused = false;
        startBtn.style.display = "none";
        stopBtn.style.display = "block";
        //console.log(this.paused);
      } else {
        this.paused = true;
        startBtn.style.display = "block";
        stopBtn.style.display = "none";
        //console.log(this.paused);
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
  grid-template-rows: 100px 1fr 5fr 1fr 1fr;
  height: 100vh;
  align-items: center;
  justify-items: center;
  color: white;
  display: grid;
  width: 100vw;
  position: fixed;
  z-index: 0;
  transition: opacity ease-in-out 1s;
}

#settings-toggle {
  grid-column: 1;
  width: 35px;
  align-self: center;
  justify-self: center;
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
  opacity: 0.6;
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
#reset-btn {
  align-self: center;
  border: 1px solid white;
  padding: 5px 10px;
  border-radius: 5px;
}

#reset-btn:hover {
  background-color: white;
  color: black;
  cursor: pointer;
}

@media screen and (max-width: 700px) {
  #settings-toggle {
    grid-row: 1;
  }
}
</style>
