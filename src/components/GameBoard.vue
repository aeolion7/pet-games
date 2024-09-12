<script setup>
import BoardTile from './BoardTile.vue';
import { ref } from 'vue';

const numTiles = ref(24);

const tileNames = ["BoulderHills", "CrystalCove", "MistyMountain", "PebbleBeach", "RoaringRapids", "RockslideValley", "SunnyMeadow", "WindyCliffs", "WistfulWoods"];

const boardLayout = [{ tileName: "Start", id: "start-0" }];

for (let idx = 1; idx < numTiles.value - 1; idx++) {
  const newTileName = tileNames[Math.floor(Math.random() * tileNames.length)];
  boardLayout.push({ tileName: newTileName, id: `${newTileName}-${idx}` })
}

boardLayout.push({ tileName: "End", id: "end-23" });
</script>

<template>
  <div id="game-board">
    <div id="grid">
      <BoardTile v-for="tile in boardLayout" :key="tile.id" :tile-name="tile.tileName" />
    </div>
  </div>
</template>

<style>
#game-board {
  display: flex;
  justify-content: center;
  height: inherit;
  width: inherit;
}

#grid {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  grid-template-rows: repeat(4, 1fr);
  height: 70vh;
  width: 70vw;
}
</style>
