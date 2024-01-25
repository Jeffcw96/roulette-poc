<script setup>
import Wheel from "./components/Wheel.vue";
import BetTable from "./components/BetTable.vue";
import Actions from "./components/Actions.vue";
import { ref } from "vue";

let isAnimationRunning = ref(false);
const startRolling = () => {
  isAnimationRunning.value = true;
};

const isProcessFinished = () => {
  isAnimationRunning.value = false;
};
</script>

<template>
  <main>
    <div class="game-container">
      <Wheel
        :isAnimationRunning="isAnimationRunning"
        @isProcessFinished="isProcessFinished"
      />
      <BetTable :isAnimationRunning="isAnimationRunning" />
      <Actions @startRolling="startRolling" />
    </div>
  </main>
</template>

<style scoped>
.game-container {
  max-width: 720px;
  margin: 0 auto;
}

.animation-blocker {
  min-height: 100vh;
  width: 100%;
  position: fixed;
  z-index: 99;
}

main {
  min-height: 100vh;
  background-color: #0e3c04;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
