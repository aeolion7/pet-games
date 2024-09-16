<script setup>
const props = defineProps({
  tileName: String,
  isFlipped: Boolean,
  isOpaque: Boolean
});

const monsters = [
  { name: "Fogwing Wyvern", element: "Air", power: 4, terrainType: "MistyMountain" },
  { name: "Diving Sky Dancer", element: "Air", power: 3, terrainType: "CloudyPass" },
  { name: "Rock Roc Bird", element: "Air / Rock", power: 6, terrainType: "WindyCliffs" },
  { name: "Hungry Goat", element: "Grass", power: 5, terrainType: "SunnyMeadow" },
  { name: "Bramblebeast", element: "Grass", power: 6, terrainType: "WistfulWoods" },
  { name: "Clawsome Crab", element: "Rock / Water", power: 4, terrainType: "PebbleBeach" },
  { name: "Rocky Golem", element: "Rock", power: 5, terrainType: "RockslideValley" },
  { name: "Stony Armadillo", element: "Rock", power: 4, terrainType: "BoulderHills" },
  { name: "Cliff Hawk", element: "Grass / Air", power: 7, terrainType: "NarrowCanyon" },
  { name: "Raging Crocodile", element: "Water", power: 8, terrainType: "RoaringRapids" },
  { name: "Algae Enforcer", element: "Water", power: 6, terrainType: "CrystalCove" },
  { name: "Giant Toad", element: "Water / Grass", power: 5, terrainType: "QuicksandBog" }
];

function getTileImageUrl(tileName, isFlipped) {
  if (isFlipped) {
    return require('../assets/tiles/reverse/' + tileName + '.png');
  } else {
    return require('../assets/tiles/' + tileName + '.png');
  }
}

function showMonsterName() {
  if (props.isFlipped) return;
  const monsterName = monsters.find(monster => monster.terrainType === props.tileName).name;
  alert(monsterName);
}

const imgUrl = getTileImageUrl(props.tileName, props.isFlipped);
</script>

<template>
  <img class="tile" @click="showMonsterName" :class="props.isOpaque ? 'is-opaque' : ''" :src="imgUrl">
</template>

<style>
:root {
  --tile-width: 24vw;
  --tile-height: 32vh;
  --horizontal-tile-offset: calc(var(--tile-width) / 4);
  --vertical-tile-offset: calc(var(--tile-height) / 2);
}

.test {
  position: fixed;
  color: red;
}

.tile {
  width: var(--tile-width);
  height: var(--tile-height);
  position: relative;
}

.tile:not(.is-opaque) {
  opacity: 30%;
}

.tile:nth-child(1) {
  left: calc(2 * var(--horizontal-tile-offset));
}

.tile:nth-child(2) {
  left: var(--horizontal-tile-offset);
  top: var(--vertical-tile-offset);
}

.tile:nth-child(4) {
  right: var(--horizontal-tile-offset);
  bottom: var(--vertical-tile-offset);
}

.tile:nth-child(5) {
  right: calc(2 * var(--horizontal-tile-offset));
}
</style>
