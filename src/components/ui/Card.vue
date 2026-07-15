<script setup>
import { ref, computed } from "vue";
import RightIcon from "../../assets/icons/RightIcon.vue";
import WrongIcon from "../../assets/icons/WrongIcon.vue";

const props = defineProps({
  num: {
    type: Number,
    default: 1,
  },
  word: {
    type: String,
    default: "null",
  },
  translation: {
    type: String,
    default: "Пусто",
  },
});

const isFlipped = ref(false);
const status = ref("pending"); // success | fail | pending

// Форматирование номера (01, 02...)
const formattedNum = computed(() => {
  return props.num < 10 ? `0${props.num}` : props.num;
});

const handleAnswer = (correct) => {
  status.value = correct ? "success" : "fail";
};
</script>

<template>
  <div class="card-container">
    <div class="card" :class="{ 'is-flipped': isFlipped }">
      <!-- FRONT -->
      <div class="card__side card__front" @click="isFlipped = true">
        <div class="card__wrapper">
          <p class="card__number">{{ formattedNum }}</p>
          <p class="card__txt">{{ word }}</p>
          <p class="card__subtxt">Перевернуть</p>
        </div>
      </div>

      <!-- BACK -->
      <div class="card__side card__back">
        <div class="card__wrapper">
          <!-- Статус ответа -->
          <template v-if="status !== 'pending'">
            <component
              :is="status === 'success' ? RightIcon : WrongIcon"
              width="40"
              height="40"
              class="card__icon"
            />
          </template>

          <p class="card__number">{{ formattedNum }}</p>
          <p class="card__txt">{{ translation }}</p>


          <!-- Кнопки выбора -->
          <div v-if="status === 'pending'" class="card__btns">
            <RightIcon class="btn-icon" @click="handleAnswer(true)" />
            <WrongIcon class="btn-icon" @click="handleAnswer(false)" />
          </div>

          <p v-else class="card__subtxt">Завершено</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Ваши стили остаются прежними, можно добавить курсор для кнопок */
.btn-icon {
  cursor: pointer;
  transition: transform 0.2s;
}
.btn-icon:hover {
  transform: scale(1.2);
}

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
