<script setup>
const props = defineProps({
  tileName: String,
  isFlipped: Boolean,
  isOpaque: Boolean
});

function getTileImageUrl(tileName, isFlipped) {
  if (isFlipped) {
    return require('../assets/tiles/reverse/' + tileName + '.png');
  } else {
    return require('../assets/tiles/' + tileName + '.png');
  }
}

const imgUrl = getTileImageUrl(props.tileName, props.isFlipped);
</script>

<template>
  <img class="tile" :class="props.isOpaque ? 'is-opaque' : ''" :src="imgUrl">
</template>

<style>
:root {
  --tile-width: 24vw;
  --tile-height: 32vh;
  --horizontal-tile-offset: calc(var(--tile-width) / 4);
  --vertical-tile-offset: calc(var(--tile-height) / 2);
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
