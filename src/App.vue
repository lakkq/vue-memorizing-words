<script setup>
import { ref } from "vue";
import AppHeader from "./components/layout/AppHeader.vue";
import Button from "./components/ui/Button.vue";
import Card from "./components/ui/Card.vue";
import { cardsData } from "./data/cards";

const cards = ref(cardsData);
const score = ref(0);

</script>

<template>
  <AppHeader :score />
  <Button>Начать игру</Button>
  <div class="cards-list">
    <Card
      v-for="card in cards"
      :key="card.id"
      :num="card.id"
      :word="card.word"
      :translation="card.translation"
    />
  </div>
</template>

<style scoped>
.cards-list {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  padding: 20px;
  justify-content: center;
}
</style>
