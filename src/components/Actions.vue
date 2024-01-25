<script setup>
const emit = defineEmits(["startRolling"]);
const props = defineProps(["isAnimationRunning"]);

const startRolling = () => {
  if (!props.isAnimationRunning) {
    emit("startRolling");
  }
};
</script>

<template>
  <div class="action-menu">
    <button class="refresh" @click="startRolling">
      <img src="../assets/refresh.svg" class="primary" />
    </button>
  </div>
</template>

<style scoped>
.action-menu {
  position: fixed;
  right: 0;
  bottom: 10vh;
}
.refresh {
  border: 1px solid transparent;
  border-radius: 100%;
}

.refresh > img {
  width: 15vw;
  max-width: 6.25rem;
}
</style>
