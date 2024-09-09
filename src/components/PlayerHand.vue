<script setup>
import { ref } from 'vue';
const numCards = ref(5);
</script>

<template>
  <div id="player-hand">
    <p>Player Hand placeholder</p>
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
</style>
