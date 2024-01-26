<template>
  <div class="progress-container">
    <svg class="circle" width="200" viewBox="0 0 20 20">
      <circle class="bg" cx="10" cy="10" r="8" />
      <circle
        class="progress"
        cx="10"
        cy="10"
        r="8"
        :style="{
          strokeDasharray: '51 51',
          strokeDashoffset: circleValue,
        }"
        transform="rotate(-90 10 10)"
      />
      <text x="50%" y="60%">{{ progress }}%</text>
    </svg>
  </div>
</template>

<script>
export default {
  data() {
    return {
      circleValue: 0,
      progress: 0,
      isInProgress: false,
    };
  },
  props: {
    progressValue: {
      default: true,
      type: Boolean,
      validator: (value) => typeof value === "boolean",
    },
  },
  watch: {
    progressValue(val) {
      if (val) {
        this.isInProgress = true;
        this.fakeLoader();
      } else {
        this.resetLoader();
      }
    },
  },
  methods: {
    fakeLoader() {
      const vm = this;
      let progress = 0;

      function simulateLoading() {
        if (progress <= 100 && vm.isInProgress) {
          setTimeout(() => {
            vm.circleValue = -51 - (51 / 100) * progress;
            vm.progress = progress;
            progress += 1;
            simulateLoading();
          }, 20); // Adjust the delay (in milliseconds) as needed
        } else {
          vm.resetLoader();
        }
      }

      simulateLoading();
    },
    resetLoader() {
      this.circleValue = 0;
      this.progress = 0;
      this.isInProgress = false;
    },
  },
};
</script>

<style scoped>
.progress-container {
  background-color: rgb(0, 16, 80);
  padding: 20px;
  border-radius: 20px;
}

.circle {
  .bg {
    fill: none;
    stroke: #676767;
    stroke-width: 2;
  }

  .progress {
    fill: none;
    stroke: #feef1f;
    stroke-width: 2;
    stroke-linecap: round;
    filter: drop-shadow(0 0 1px rgba(254, 239, 31, 30));
  }

  text {
    font-size: 5px;
    text-anchor: middle;
    fill: #feef1f;
  }
}
</style>
