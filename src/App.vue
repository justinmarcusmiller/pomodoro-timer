<template>
  <div id="app">
    <Settings
      :workTime="workTime"
      :shortBreakTime="shortBreakTime"
      :longBreakTime="longBreakTime"
      :themeColor="themeColor"
      @workTimeChanged="workTime = $event"
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
    Settings
  },
  data() {
    return {
      workTime: 1,
      shortBreakTime: 0,
      longBreakTime: 0,
      themeColor: "blue"
    };
  },
  methods: {

  }
};
</script>

<style>
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
</style>
