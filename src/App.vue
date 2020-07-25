<template>
  <div id="app">
    <transition name="fade">
      <Settings
        v-if="showSettings === true"
        :workTime="workTime"
        :breakTime="breakTime"
        :themeColor="themeColor"
        @workTimeChanged="workTime = $event"
        @breakTimeChanged="breakTime = $event"
        @themeChanged="themeColor = $event"
        @showSettings="showSettings = $event"
      />
    </transition>
    <Clock
      :workTime="workTime"
      :breakTime="breakTime"
      :themeColor="themeColor"
      :paused="paused"
      @showSettings="showSettings = $event"
      :timeRemaining="timeRemaining"
      :mode="mode"
    />
  </div>
</template>

<script>
import Clock from "@/components/Clock.vue";
import Settings from "@/components/Settings.vue";

export default {
  name: "App",
  components: {
    Clock,
    Settings,
  },
  data() {
    return {
      workTime: 15,
      breakTime: 5,
      themeColor: "blue",
      showSettings: false,
      paused: true,
      mode: "work",
      timeRemaining: (this.workTime * 60),
    };
  },
  created: function () {
    this.timeRemaining = (this.workTime * 60)
  },
  watch: {
    workTime: function() {
      //console.log("workTime changed");
      this.timeRemaining = (this.workTime * 60)
      //console.log(this.timeRemaining)
      this.paused = true;
      let stopBtn = document.getElementById("stop-btn");
      let startBtn = document.getElementById("start-btn");
      startBtn.style.display = "block";
      stopBtn.style.display = "none";
      //console.log(this.paused);
    },
  },
  methods: {},
};
</script>

<style>
* {
  box-sizing: border-box;
}
body {
  margin: 0;
  font-size: 16px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  margin: 0;
  font-size: 16px;
}

.blue {
  background-color: #4299e1;
}

.black {
  background-color: #1a202c;
}

.green {
  background-color: #48bb78;
}

.yellow {
  background-color: #f6e05e;
}

.red {
  background-color: #e53e3e;
}

.orange {
  background-color: #dd6b20;
}

.gray {
  background-color: #a0aec0;
}

.purple {
  background-color: #805ad5;
}

.pink {
  background-color: #f687b3;
}

.brown {
  background-color: #744210;
}

.darkblue {
  background-color: #2c5282;
}

.lightblue {
  background-color: #90cdf4;
}

.block {
  display: block;
}

.grid {
  display: grid;
  width: 100vw;
  justify-content: center;
}

.hidden {
  display: none;
}

#time-remaining {
  grid-row: 1;
  grid-column: 2;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 100ms ease-out;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
