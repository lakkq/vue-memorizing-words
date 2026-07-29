<script setup>
import { onBeforeMount, ref } from "vue";
import AppHeader from "./components/layout/AppHeader.vue";
import Button from "./components/ui/Button.vue";
import Card from "./components/ui/Card.vue";
import { cardsData } from "./data/cards";

const cards = ref([]);
const score = ref(0);

const fetchCards = async () => {
  try {
    const response = await fetch("http://localhost:8080/api/random-words");
    if (response.ok) {
      const cardsList = await response.json();
      cards.value = cardsList.map((card) => ({
        ...card,
        state: "pending",
        status: "pending",
        id: cardsList.indexOf(card) + 1,
      }));
    } else {
      console.warn("Сервер ответил с ошибкой");
    }
  } catch (error) {
    console.error("Ошибка при загрузке карт:", error);
  }
};

const startButton = () => {
  fetchCards();
  cards.value = cards.value.map((card) => ({
    ...card,
    state: "pending",
    status: "pending",
  }));
};

const answerHandler = (card, stat) => {
  console.log(stat)
  stat === 'success' ? score.value += 10 : score.value -= 4
  card.status = stat
};
</script>

<template>
  <AppHeader :score />
  <Button v-if="!cards.length" @click="startButton">Начать игру</Button>
  <div class="cards-list">
    <Card
      v-if="cards.length"
      v-for="card in cards"
      v-bind="card"
      @flip-card="card.state = 'flipped'"
      @answer-card="(stat) => answerHandler(card, stat)"
    />
  </div>
  <Button v-if="cards.length" @click="startButton">Начать заново</Button>
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
