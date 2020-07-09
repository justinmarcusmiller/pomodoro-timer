<template>
  <div id="settings">
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
    <div id="settings-grid">
      <div class="setting-block-sm" v-bind:class="themeColor">
        <input
          type="number"
          :value="workTime"
          @input="changeWorkTime"
          max="60"
          min="1"
        />
        <label for="work-time">Work Time</label>
      </div>
      <div class="setting-block-sm" v-bind:class="themeColor">
        <input
          type="number"
          value="5"
          @input="changeShortBreakTime"
          max="60"
          min="1"
        />
        <label for="short-break-time">Short Break</label>
      </div>
      <div class="setting-block-sm" v-bind:class="themeColor">
        <input
          type="number"
          value="15"
          @input="changeLongBreakTime"
          max="60"
          min="1"
        />
        <label for="long-break-time">Long Break</label>
      </div>
      <div class="setting-block-md" v-bind:class="themeColor">
        <input type="number" />
        <label for="numOfSessions">Number Of Sessions</label>
      </div>
    </div>

    <h2>Theme Color</h2>
    <div id="color-grid" v-bind:class="themeColor">
      <div class="color-block red" @click="changeTheme(`red`)"></div>
      <div class="color-block orange" @click="changeTheme(`orange`)"></div>
      <div class="color-block green" @click="changeTheme(`green`)"></div>
      <div class="color-block blue" @click="changeTheme(`blue`)"></div>
      <div class="color-block yellow" @click="changeTheme(`yellow`)"></div>
      <div class="color-block gray" @click="changeTheme(`gray`)"></div>
      <div class="color-block purple" @click="changeTheme(`purple`)"></div>
      <div class="color-block pink" @click="changeTheme(`pink`)"></div>
      <div class="color-block brown" @click="changeTheme(`brown`)"></div>
      <div class="color-block darkblue" @click="changeTheme(`darkblue`)"></div>
      <div
        class="color-block lightblue"
        @click="changeTheme(`lightblue`)"
      ></div>
      <div class="color-block black" @click="changeTheme(`black`)"></div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["workTime", "shortBreakTime", "longBreakTime", "themeColor"],
  methods: {
    changeTheme(color) {
      console.log(color);
      this.themeColor = color;
      this.$emit("themeChanged", this.themeColor);
    },
    changeWorkTime(event) {
      this.workTime = event.target.value;
      this.$emit("workTimeChanged", this.workTime);
    },
    changeShortBreakTime(event) {
      this.shortBreakTime = event.target.value;
      this.$emit("shortBreakTimeChanged", this.shortBreakTime);
    },
    changeLongBreakTime(event) {
      this.longBreakTimee = event.target.value;
      this.$emit("longBreakTimeChanged", this.longBreakTime);
    },
    toggleSettings() {
      clock.style.display = "grid";
      settings.style.display = "none";
    },
  },
};
</script>

<style>
#settings {
  display: none;
  width: 100%;
  justify-content: center;
}

#settings-grid {
  display: grid;
  grid-gap: 15px;
  justify-items: center;
  align-items: center;
}

h2 {
  grid-column: 1 / 4;
}

.setting-block-sm {
  grid-column: auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
  border-radius: 5px;
  width: 100%;
  height: 150px;
  color: white;
  font-weight: 600;
}

.setting-block-sm input {
  font-weight: 600;
  font-size: 24px;
  color: white;
}

.setting-block-md {
  color: white;
  font-weight: 600;
  grid-column: 1 / 4;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
  border-radius: 5px;
  width: 100%;
  height: 150px;
}

input[type="number"] {
  background: none;
  border: none;
  text-align: right;
  width: 45px;
}

input[type="number" i] {
  font-weight: 600;
  text-align: center;
}

#exit-btn {
  grid-column: 1;
  width: 45px;
  align-self: center;
  justify-self: flex-start;
  margin-top: 5px;
}

.color-block {
  grid-column: auto;
  padding: 5px;
  display: flex;
  width: 20vw;
  height: 10vw;
  max-width: 250px;
  max-height: 150px;
  border-radius: 5px;
  transition: opacity ease-in-out 0.1s;
  border: 2px solid white;
}

.color-block:hover {
  opacity: 0.8;
}

#color-grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr;
  grid-gap: 15px;
  padding: 15px;
  border-radius: 5px;
  justify-items: center;
}

@media screen and (max-width: 700px) {
  #color-grid {
    grid-template-columns: 1fr 1fr 1fr;
    margin-bottom: 15px;
  }

  .setting-block-sm {
    height: 100px;
  }

  .setting-block-md {
    height: 100px;
  }

  #exit-btn {
    margin-top: 15px;
  }
}
</style>
