<script setup>
import { ref } from "vue";
import AppHeader from "./components/layout/AppHeader.vue";
import Button from "./components/ui/Button.vue";
import Card from "./components/ui/Card.vue";
import { cardsData } from "./data/cards";

const cards = ref(cardsData);
const score = ref(0);

// Для демонстрации выводим первую карту
const currentCard = ref(cards.value[0]);
</script>

<template>
  <AppHeader />
  <div class="game-info">
    <span>Очки: {{ score }}</span>
  </div>
  <Button>Начать игру</Button>
  <div class="cards-list">
    <Card
      v-if="currentCard"
      :num="currentCard.id"
      :word="currentCard.word"
      :translation="currentCard.translation"
    />
  </div>
</template>

<style scoped>
.game-info {
  text-align: center;
  margin: 10px 0;
  font-weight: bold;
}
.cards-list {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  padding: 20px;
  justify-content: center;
}
</style>
