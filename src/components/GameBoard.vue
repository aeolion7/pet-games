<script setup>
import { ref } from 'vue';

const numTiles = ref(24);
</script>

<template>
  <div id="game-board">
    <p>GameBoard placeholder</p>
    <p>The game will have {{ numTiles }} tiles.</p>
  </div>
</template>

<style>
#game-board {
  height: inherit;
  width: inherit;
}
</style>
