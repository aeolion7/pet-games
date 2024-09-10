<script setup>
const props = defineProps({
  petName: {
    default: "Bananakeet",
    type: String
  },
  toolName: {
    default: "RockCandy",
    type: String
  },
  cardType: {
    type: String,
    required: true
  }
});

function getCreatureImageUrl(petName) {
  return require('../assets/cards/creatures/' + petName + '.jpg');
}

function getEquipmentImageUrl(toolName) {
  return require('../assets/cards/equipment/' + toolName + '.jpg');
}

const imgUrl = props.cardType === "creature" ? getCreatureImageUrl(props.petName) : getEquipmentImageUrl(props.toolName);
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
