<script setup>
const props = defineProps({
  name: {
    type: String,
    required: true
  },
  cardType: {
    type: String,
    required: true
  }
});

function getCreatureImageUrl(name) {
  return require('../assets/cards/creatures/' + name + '.jpg');
}

function getEquipmentImageUrl(name) {
  return require('../assets/cards/equipment/' + name + '.jpg');
}

const imgUrl = props.cardType === "creature" ? getCreatureImageUrl(props.name) : getEquipmentImageUrl(props.name);
</script>

<template>
  <img class="card" :src="imgUrl">
</template>

<style scoped>
.card {
  margin: 2px;
  width: 10%;
}
</style>
