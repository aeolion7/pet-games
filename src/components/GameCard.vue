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

const imgUrl = props.cardType === "creature"
  ? require('../assets/cards/creatures/' + props.name + '.jpg')
  : require('../assets/cards/equipment/' + props.name + '.jpg');
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
