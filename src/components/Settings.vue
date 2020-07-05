<template>
  <div id="settings" class="hidden">
    <div id="exit-btn" @click="toggleSettings">
      <svg fill="currentColor" viewBox="0 0 20 20">
        <path
          fill-rule="evenodd"
          d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z"
          clip-rule="evenodd"
        ></path>
      </svg>
    </div>
    <h2>Time</h2>
    <div class="setting-block-sm">
      <input type="number" :value="workTime" @input="changeWorkTime" max="60" min="1" />
      <label for="work-time">Work Time</label>
    </div>
    <div class="setting-block-sm">
      <input type="number" value="5" max="60" min="1" />
      <label for="short-break-time">Short Break</label>
    </div>
    <div class="setting-block-sm">
      <input type="number" value="15" max="60" min="1" />
      <label for="long-break-time">Long Break</label>
    </div>
    <div class="setting-block-md">
      <input type="number" />
      <label for="numOfSessions">Number Of Sessions</label>
    </div>
    <h2>Theme Color</h2>
  </div>
</template>

<script>
export default {
  props: ["workTime", "shortBreakTime", "longBreakTime", "themeColor"],
  data() {
    return {
      newWorkTime: 0,
    }
  },
  methods: {
    changeWorkTime(event) {
      this.workTime = event.target.value;
      this.$emit('workTimeChanged', this.workTime);
    },
    toggleSettings() {
      let settings = document.getElementById("settings");
      settings.classList.toggle("hidden");
      settings.classList.toggle("grid");
      clock.classList.toggle("grid");
      clock.classList.toggle("hidden")
    },
  },
};
</script>

<style>
#settings {
  grid-gap: 15px;
  justify-items: center;
  align-items: center;
  padding: 0 15px;
}

h2 {
  grid-column: 1 / 4;
}

.setting-block-sm {
  grid-column: auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
  padding: 5px;
  background-color: cadetblue;
  border-radius: 5px;
  width: 100%;
  height: 100px;
}

.setting-block-md {
  grid-column: 1 / 4;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
  padding: 5px;
  background-color: cadetblue;
  border-radius: 5px;
  width: 100%;
  height: 100px;
}

input[type="number"] {
  background: none;
  border: none;
  text-align: right;
  width: 45px;
}

input[type="number" i] {
  padding-right: 2px;
  font-weight: 600;
}

#exit-btn {
  grid-column: 1;
  width: 45px;
  align-self: center;
  justify-self: flex-start;
}
</style>
