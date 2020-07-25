<template>
  <div id="settings">
    <div id="settings-toggle" @click="hideSettings">
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
          @input="changeBreakTime"
          max="60"
          min="1"
        />
        <label for="break-time">Break</label>
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
  props: ["workTime", "breakTime", "themeColor"],
  methods: {
    changeTheme(color) {
      //console.log(color);
      this.themeColor = color;
      this.$emit("themeChanged", this.themeColor);
    },
    changeWorkTime(event) {
      this.workTime = event.target.value;
      this.$emit("workTimeChanged", this.workTime);
    },
    changeBreakTime(event) {
      this.breakTimee = event.target.value;
      this.$emit("breakTimeChanged", this.breakTime);
    },
    hideSettings() {
      this.$emit("showSettings", false);
    },
  },
};
</script>

<style>
#settings {
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 100px auto auto auto auto;
  height: 100vh;
  align-items: center;
  justify-items: center;
  justify-content: center;
  display: grid;
  width: 100vw;
  background-color: white;
  z-index: 1;
  min-height: 100vh;
  /* padding: 15px; */
  transition: opacity ease-in-out 1s;
}

#settings-grid {
  display: flex;
  justify-items: center;
  align-items: center;
  grid-column: 1 / 4;
  grid-row: 3;
  width: 100%;
  height: 100%;
  max-width: 1000px;
}

.setting-block-sm {
  grid-column: auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
  border-radius: 5px;
  width: 100%;
  margin: 15px;
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
  width: 35px;
  align-self: center;
  justify-self: center;
}

.color-block {
  grid-column: auto;
  padding: 5px;
  display: flex;
  width: 100%;
  height: 100%;
  max-width: 250px;
  max-height: 150px;
  border-radius: 5px;
  transition: opacity ease-in-out 0.1s;
  border: 2px solid white;
}

.color-block:hover {
  opacity: 0.8;
}

h2 {
  grid-column: 1 / 4;
}

#color-grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: 100px 100px 100px;
  grid-gap: 15px;
  padding: 15px;
  border-radius: 5px;
  justify-items: center;
  grid-column: 1 / 4;
  grid-row: 5;
  width: 96%;
  max-width: 1000px;;
}

@media screen and (max-width: 700px) {
  #color-grid {
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 100px 100px 100px 100px;
  }

  #settings {
    height: 100%;
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
