<template>
  <div id="app">
    <Settings
      :workTime="workTime"
      :shortBreakTime="shortBreakTime"
      :longBreakTime="longBreakTime"
      :themeColor="themeColor"
      @workTimeChanged="workTime = $event"
      @shortBreakTimeChanged="shortBreakTime = $event"
      @longBreakTimeChanged="longBreakTime = $event"
      @themeChanged="themeColor = $event"
    />
    <Clock
      :workTime="workTime"
      :shortBreakTime="shortBreakTime"
      :longBreakTime="longBreakTime"
      :themeColor="themeColor"
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
      workTime: 1,
      shortBreakTime: 5,
      longBreakTime: 15,
      themeColor: "blue",
    };
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
</style>
