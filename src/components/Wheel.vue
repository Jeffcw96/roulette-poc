<script setup>
import { ref, watch } from "vue";

const props = defineProps(["isAnimationRunning"]);
const emit = defineEmits(["isProcessFinished"]);
const rolling = ref(false);
const showWheel = ref(false);
const isAnimationRunning = ref(props.isAnimationRunning);
let result = "";
const generateRandomNumber = () => {
  return Math.round(Math.random() * 36);
};
const stopRolling = () => {
  rolling.value = false;
  result = String(generateRandomNumber());
};
const finish = () => {
  result = "";
  emit("isProcessFinished");
};

const delay = (time) => new Promise((resolve) => setTimeout(resolve, time));
watch(
  () => props.isAnimationRunning,
  async (newVal, oldVal) => {
    isAnimationRunning.value = newVal;
    showWheel.value = newVal;

    // Rolling is start
    if (!oldVal && newVal) {
      rolling.value = true;
      await delay(3000);
      stopRolling();

      await delay(3000);
      finish();
    }
  },
  { immediate: true }
);
</script>

<template>
  <div class="relative">
    <div class="wheel-container" :class="showWheel ? 'show' : 'hide'">
      <img
        src="../assets/wheel.jpeg"
        class="wheel"
        alt="wheel"
        :class="rolling ? 'rolling' : ''"
      />
    </div>
    <div class="result">{{ result }}</div>
  </div>
</template>

<style scoped>
.relative {
  position: relative;
}

.result {
  font-size: 1.5rem;
  font-weight: bold;
  color: white;
  text-align: right;
  position: absolute;
  right: 0;
  bottom: 0;
}
.show {
  transform: translate(0, 0);
}

.hide {
  transform: translate(0, -50vh);
}

.wheel {
  animation: rotate 3s infinite linear;
  max-height: 45vh;
  max-width: 50%;
  animation-play-state: paused;
}

.wheel.rolling {
  animation-play-state: running !important;
}

.wheel-container {
  transition: all 1s;
  text-align: center;
}

@keyframes rotate {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

@media only screen and (min-width: 650px) {
  .wheel {
    max-width: 70%;
  }
  .wheel-container {
    transform: translate(0, 0) !important;
  }
}
</style>
