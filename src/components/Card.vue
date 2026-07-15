<template>
  <div class="card-container" @click="isFlipped = !isFlipped">
    <div class="card" :class="{ 'is-flipped': isFlipped }">
      <!-- Лицевая сторона -->
      <div class="card-side card-front">
        <slot name="front">
          <span>Front Side</span>
        </slot>
      </div>

      <!-- Обратная сторона -->
      <div class="card-side card-back">
        <slot name="back">
          <span>Back Side</span>
        </slot>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const isFlipped = ref(false);
</script>

<style scoped>
.card-container {
  width: 300px;
  height: 200px;
  perspective: 1000px;
  cursor: pointer;
  margin: 20px;
}

.card {
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 0.6s cubic-bezier(0.4, 0, 0.2, 1);
  transform-style: preserve-3d;
}

.card.is-flipped {
  transform: rotateY(180deg);
}

.card-side {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 12px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  font-size: 1.5rem;
  padding: 20px;
  box-sizing: border-box;
}

.card-front {
  background-color: #ffffff;
  color: #333;
}

.card-back {
  background-color: var(--button-color, #42b983);
  color: white;
  transform: rotateY(180deg);
}
</style>
