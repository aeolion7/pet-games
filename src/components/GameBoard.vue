<script setup>
import BoardTile from './BoardTile.vue';
import { ref } from 'vue';

const numTiles = ref(5);

const tileNames = ["BoulderHills", "CrystalCove", "MistyMountain", "PebbleBeach", "RoaringRapids", "RockslideValley", "SunnyMeadow", "WindyCliffs", "WistfulWoods"];

const boardLayout = [];

for (let idx = 0; idx < numTiles.value; idx++) {
  const newTileName = tileNames[Math.floor(Math.random() * tileNames.length)];
  boardLayout.push({ tileName: newTileName, id: `${newTileName}-${idx}` })
}
</script>

<template>
  <div id="game-board">
    <BoardTile v-for="tile in boardLayout" :key="tile.id" :tile-name="tile.tileName" />
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
