<script setup>
import { reactive, ref, watch } from "vue";
import { rouletteNumber } from "../static/number";
const props = defineProps(["isAnimationRunning"]);
const numbers = reactive(rouletteNumber);
const isAnimationRunning = ref(props.isAnimationRunning);
const divs = ref([]);

watch(
  () => props.isAnimationRunning,
  (newVal) => {
    isAnimationRunning.value = newVal;
  },
  { immediate: true }
);
</script>
<template>
  <div class="bet-container" :class="isAnimationRunning ? 'animating' : ''">
    <div class="other-category">
      <div>1 ~ 18</div>
      <div>Even</div>
      <div>
        <div class="red box"></div>
      </div>
      <div>
        <div class="black box"></div>
      </div>
      <div>Odd</div>
      <div>19~36</div>
    </div>
    <div class="twelve-factor">
      <div>1st 12</div>
      <div>2nd 12</div>
      <div>3rd 12</div>
    </div>
    <div class="green-red-table">
      <div class="zero">0</div>
      <div
        v-for="(number, index) in numbers"
        :key="number.label"
        class="number"
        :style="{ backgroundColor: number.color }"
        :ref="
          (el) => {
            divs[index] = el;
          }
        "
      >
        {{ number.label }}
      </div>
      <div class="two-per-one">2 ~ 1</div>
      <div class="two-per-one">2 ~ 1</div>
      <div class="two-per-one">2 ~ 1</div>
    </div>
    <div></div>
  </div>
</template>
<style scoped>
.animating {
  scale: 0.7;
  bottom: 10vh !important;
}

.two-per-one {
  font-weight: bold;
  text-align: center;
  color: white;
  font-size: 1.1rem;
  border: 1px solid white;
  width: 11vw;
  padding: 1rem 0;
}

.box {
  width: 35%;
  height: 2vh;
  display: flex;
  justify-content: center;
  align-items: center;
  transform: matrix(2, 2, -1, 1, 6, 28);
}

.red {
  background: red;
}

.black {
  background: black;
}

.twelve-factor,
.other-category {
  display: flex;
  justify-content: center;
  flex-direction: column;
}

.other-category > div {
  font-weight: bold;
  text-align: center;
  color: white;
  font-size: 1.1rem;
  border: 1px solid white;
  writing-mode: vertical-lr;
  height: 9vh;
  padding: 0 0.75rem;
}
.twelve-factor > div {
  font-weight: bold;
  text-align: center;
  color: white;
  font-size: 1.1rem;
  border: 1px solid white;
  writing-mode: vertical-lr;
  height: 20vh;
  padding: 0 0.75rem;
}

.bet-container {
  position: relative;
  display: flex;
  justify-content: center;
  padding-top: 2rem;
  transition: all 1s;
  bottom: 25vh;
}

.zero {
  color: white;
  width: 100%;
  text-align: center;
  padding: 1rem 0;
  border: 1px solid white;
}

.green-red-table {
  display: flex;
  width: 33vw;
  flex-wrap: wrap;
  justify-content: center;
}

.green-red-table > .number {
  /* Add your specific styling for child elements */
  border: 1px solid white;
  display: flex;
  justify-content: center;
  align-items: center;
  color: white;
  width: 11vw;
  height: 5vh;
}

@media only screen and (min-width: 650px) {
  .animating {
    scale: 1;
    bottom: 10vh !important;
  }
  .bet-container {
    transform: rotate(270deg);
    bottom: 10vh;
  }
  .two-per-one {
    width: 6vw !important;
  }

  .green-red-table {
    width: 18vw;
  }

  .green-red-table > .number {
    width: 6vw;
  }
}
</style>
