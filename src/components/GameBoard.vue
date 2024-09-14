<script setup>
import BoardTile from './BoardTile.vue';
import { ref } from 'vue';

const numTiles = ref(5);
const boardLayout = ref([]);
const currentTileIdx = ref(0);

const tileNames = ["BoulderHills", "CrystalCove", "MistyMountain", "PebbleBeach", "RoaringRapids", "RockslideValley", "SunnyMeadow", "WindyCliffs", "WistfulWoods"];

for (let idx = 0; idx < numTiles.value; idx++) {
  const newTileName = tileNames[Math.floor(Math.random() * tileNames.length)];
  const tileObject = { tileName: newTileName, isFlipped: false };

  tileObject.isOpaque = idx === 0 ? true : false;

  boardLayout.value.push(tileObject);
}

function flipTile(tile) {
  tile.isFlipped = !tile.isFlipped;
}

function advanceActiveTile() {
  if (currentTileIdx.value + 1 === boardLayout.value.length) return;
  boardLayout.value[++currentTileIdx.value].isOpaque = true;
}
</script>

<template>
  <div id="game-board">
    <BoardTile v-for="(tile, index) in boardLayout" :key="index + tile.isFlipped" :tile-name="tile.tileName"
      :is-flipped="tile.isFlipped" :is-opaque="tile.isOpaque" @click="flipTile(tile)" />
  </div>
  <button class="btn--advance" @click="advanceActiveTile">Advance Tile</button>
</template>

<style>
#game-board {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 80%;
  width: inherit;
}

.btn--advance {
  position: absolute;
  left: 10px;
  bottom: 10px;
  z-index: 1;
  border: 2px solid #fff;
  margin: 5px;
  padding: 5px;
}
</style>
