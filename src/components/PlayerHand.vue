<script setup>
import { ref } from 'vue';
const numCards = ref(5);
</script>

<template>
  <div id="player-hand">
    <p>Player Hand placeholder</p>
    <button @click="numCards--">Discard</button>
    <button @click="numCards++">Draw</button>
    <p>The player's hand contains {{ numCards }} cards.</p>
  </div>
</template>

<style scoped>
#player-hand {
  position: absolute;
  text-align: center;
  width: inherit;
  bottom: 10px;
}

button {
  border: 2px solid #fff;
  margin: 5px;
  padding: 5px;
}
</style>
