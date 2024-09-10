<script setup>
const props = defineProps({
  petName: {
    default: "Bananakeet",
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

const imgUrl = props.cardType === "creature" ? getCreatureImageUrl(props.petName) : "TODO: equipment type logic here";
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
