<script setup>
import BoardTile from './BoardTile.vue';
import { ref, nextTick } from 'vue';

const numTiles = ref(5);
const boardLayout = ref([]);
const activeTileIdx = ref(0);

const tileNames = ["BoulderHills", "CrystalCove", "MistyMountain", "PebbleBeach", "RoaringRapids", "RockslideValley", "SunnyMeadow", "WindyCliffs", "WistfulWoods"];

for (let idx = 0; idx < numTiles.value; idx++) {
  const newTileName = tileNames[Math.floor(Math.random() * tileNames.length)];
  const tileObject = { tileName: newTileName, isFlipped: false };

  tileObject.isActive = idx === 0 ? true : false;

  boardLayout.value.push(tileObject);
}

function flipTile(tile) {
  tile.isFlipped = !tile.isFlipped;
}

function advanceActiveTile() {
  if (activeTileIdx.value + 1 === boardLayout.value.length) return;

  boardLayout.value[activeTileIdx.value++].isActive = false;
  boardLayout.value[activeTileIdx.value].isActive = true;
}
</script>

<template>
  <div id="game-board">
    <BoardTile v-for="(tile, index) in boardLayout" :key="index + tile.isFlipped" :tile-name="tile.tileName"
      :is-flipped="tile.isFlipped" :is-active="tile.isActive" @click="flipTile(tile)" />
  </div>
  <button @click="advanceActiveTile">Advance Tile</button>
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
