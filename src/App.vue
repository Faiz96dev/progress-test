<template>
  <div id="app">
    <ProgressBar :progressValue="fill" />
    <div class="custom-input">
      <label class="switch">
        <input v-model="fill" type="checkbox" />
        <span class="slider round"></span>
      </label>
    </div>
  </div>
</template>

<script>
import ProgressBar from "./components/ProgressBar.vue";

export default {
  name: "App",
  data() {
    return {
      fill: false,
    };
  },
  components: {
    ProgressBar,
  },
};
</script>

<style>
.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}

.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  transition: background-color 0.4s, box-shadow 0.4s;
}

.slider:before {
  content: "";
  position: absolute;
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  transition: transform 0.4s;
}

input:checked + .slider {
  background-color: rgb(0, 16, 80);
}

input:focus + .slider {
  box-shadow: 0 0 1px #2196f3;
}

input:checked + .slider:before {
  transform: translateX(26px);
}

.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.custom-input {
  display: flex;
  margin-top: 30px;
  align-items: center;
  justify-content: center;
  max-width: 100%;
}

.input {
  font-size: 20px;
  font-weight: bold;
  padding: 5px 10px;
  width: 10%;
  outline: none;
  background: #ffffff;
  color: #000000;
  border: 1px solid #c4d1eb;
  border-radius: 5px;
  box-shadow: 3px 3px 2px 0px #e2e2e2;
  transition: 0.3s ease;
}

.input:focus {
  background: #f2f2f2;
  border: 1px solid #5a7ec7;
  border-radius: 10px;
}

.input::placeholder {
  color: #dddddd;
}
</style>
