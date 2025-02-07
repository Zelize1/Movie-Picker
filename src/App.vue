<script setup>
import Randomizer from './components/Randomizer.vue';  
</script>

<template>
  <div class="nav">
    <h1 class="app-title">Movie Picker</h1>
  </div>

  <Randomizer />
</template>

<style>
.nav {
  width: 100vw;
  background-color: var(--primary-color);
}
.app-title {
  color: var(--secondary-color);
  text-align: center;
}

.randomizer {
  display: flex;
  flex-direction: column;
  width: 20vw;
}

.randomizer img {
  width: 250px;
  max-height: 300px;
  object-fit: cover;
  padding: 50px;
}
</style>
