<script setup></script>

<template>
  <button class="custom-button">
    <slot/>
  </button>
</template>

<style scoped>
.custom-button {
  background-color: var(--button-color);
  color: var(--font-color);
  font-family: var(--font);
  font-size: 24px;
  border: none;
  padding: 16px 10px;
  cursor: pointer;
  border-radius: 50px;
  min-width: 335px;
}
</style>
