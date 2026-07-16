<script setup>
import { ref } from "vue";
import Score from "../ui/Score.vue";

const { score } = defineProps({ score: Number });

</script>

<template>
  <section class="header">
    <p class="header__title">Запомни слово</p>
    <Score :value="score" />
  </section>
</template>

<style scoped>
.header {
  min-height: 100px;
  display: flex;
  justify-content: space-between;
  padding: 0 60px;
  align-items: center;
}

.header__title {
  font-size: 16px;
  text-transform: uppercase;
  font-weight: 700;
}
</style>
