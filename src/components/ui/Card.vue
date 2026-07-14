<script setup>
import { ref } from "vue";

import RightIcon from "../../assets/icons/RightIcon.vue";
import WrongIcon from "../../assets/icons/WrongIcon.vue";

const {
  num = 1,
  textEng = "null",
  textRus = "Пусто",
} = defineProps(["num", "textEng", "textRus"]);

const isFlipped = ref(false);
const isRight = ref(true);
const isAnswered = ref(false);
</script>

<template>
  <div class="card-container">
    <div class="card" :class="{ 'is-flipped': isFlipped }">
      <div class="card__side card__front" @click="isFlipped = !isFlipped">
        <div class="card__wrapper">
          <p class="card__number">
            {{ num >= 1 && num < 10 ? `0${num}` : num }}
          </p>
          <p class="card__txt">{{ textEng }}</p>
          <p class="card__subtxt">Перевернуть</p>
        </div>
      </div>

      <div class="card__side card__back">
        <div class="card__wrapper">
          <RightIcon width="40" height="40" class="card__icon" v-if="isAnswered && isRight" />
          <WrongIcon width="40" height="40" class="card__icon" v-if="isAnswered && !isRight" />
          <p class="card__number">
            {{ num >= 1 && num < 10 ? `0${num}` : num }}
          </p>
          <p class="card__txt">{{ textRus }}</p>
          <div v-if="!isAnswered" class="card__btns">
            <RightIcon @click="isAnswered = true" />
            <WrongIcon @click="isAnswered = true" />
          </div>
          <p v-if="isAnswered" class="card__subtxt">Завершено</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card-container {
  width: 250px;
  height: 376px;
  perspective: 1000px;
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

.card__side {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  background-color: #fff;
  box-shadow: 0 0 4px 0 rgba(0, 0, 0, 0.15);
  border-radius: 20px;
  padding: 28px 19px;
  box-sizing: border-box;
}

.card__front {
  z-index: 2;
  cursor: pointer;
}

.card__back {
  transform: rotateY(180deg);
}

.card__wrapper {
  border: 1px solid #cce8ff;
  width: 100%;
  height: 100%;
  border-radius: 15px;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 16px;
  box-sizing: border-box;
}

.card__number {
  padding: 0 4px;
  background-color: #fff;
  font-size: 14px;
  position: absolute;
  top: 0;
  left: 16px;
  transform: translate(0, -50%);
  text-align: center;
}

.card__txt {
  font-size: 18px;
  text-align: center;
}

.card__subtxt {
  padding: 0 4px;
  background-color: #fff;
  font-size: 12px;
  text-transform: uppercase;
  font-weight: 700;
  position: absolute;
  left: 50%;
  bottom: 0;
  transform: translate(-50%, 50%);
}

.card-container:hover .card:not(.is-flipped) {
  transform: scale(1.02);
}

.card__btns {
  display: flex;
  position: absolute;
  background-color: #fff;
  padding: 0 10px;
  bottom: 0;
  left: 50%;
  transform: translate(-50%, 50%);
  gap: 34px;
}

.card__icon {
    position: absolute;
    top: 0;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
}
</style>
