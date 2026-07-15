<script setup>
import HeartIcon from "../../assets/icons/HeartIcon.vue";
let { value = 0 } = defineProps(["value"]);
</script>

<template>
  <div class="score">
    <p class="score__num">{{ value }}</p>
    <HeartIcon class="score__icon" />
  </div>
</template>

<style scoped>
.score {
  display: flex;
  padding: 12px 24px;
  background-color: #cce8ff;
  border-radius: 100px;
  box-shadow: 0 0 4px 0 rgba(0, 0, 0, 0.15);
  gap: 10px;
}
.score__num {
    font-size: 16px;
    color: #008BFE;
    font-weight: 700;
}
</style>
