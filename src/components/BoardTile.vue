<script setup>
const props = defineProps({
  tileName: String
});

function getTileImageUrl(tileName) {
  return require('../assets/tiles/' + tileName + '.png');
}

const imgUrl = getTileImageUrl(props.tileName);
</script>

<template>
  <img class="tile" :src="imgUrl">
</template>

<style>
:root {
  --tile-width: 20vw;
  --tile-height: 30vh;
  --horizontal-tile-offset: calc(var(--tile-width) / 4);
  --vertical-tile-offset: calc(var(--tile-height) / 2);
}

.tile {
  width: var(--tile-width);
  height: var(--tile-height);
  position: relative;
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
