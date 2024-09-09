<script setup>
import GameBoard from './components/GameBoard.vue';
import PlayerHand from './components/PlayerHand.vue';
</script>

<template>
  <GameBoard />
  <PlayerHand />
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height: 100vh;
  width: 100vw;
}
</style>
