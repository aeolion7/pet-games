<script setup>
import BoardTile from './BoardTile.vue';
import { ref, nextTick } from 'vue';

const numTiles = ref(5);
const boardLayout = ref([]);

const tileNames = ["BoulderHills", "CrystalCove", "MistyMountain", "PebbleBeach", "RoaringRapids", "RockslideValley", "SunnyMeadow", "WindyCliffs", "WistfulWoods"];

for (let idx = 0; idx < numTiles.value; idx++) {
  const newTileName = tileNames[Math.floor(Math.random() * tileNames.length)];
  boardLayout.value.push({ tileName: newTileName, id: `${newTileName}-${idx}`, isFlipped: false });
}

function flipTile(tile) {
  tile.isFlipped = !tile.isFlipped;
}
</script>

<template>
  <div id="game-board">
    <BoardTile v-for="tile in boardLayout" :key="tile.id + tile.isFlipped" :tile-name="tile.tileName"
      :is-flipped="tile.isFlipped" @click="flipTile(tile)" />
  </div>
</template>

<style>
#game-board {
  display: flex;
  align-items: center;
  justify-content: center;
  height: inherit;
  width: inherit;
}
</style>
