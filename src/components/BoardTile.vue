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
