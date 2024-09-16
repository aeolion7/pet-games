<script setup>
const props = defineProps({
  name: {
    type: String,
    required: true
  },
  cardType: {
    type: String,
    required: true
  },
  power: Number
});

const imgUrl = props.cardType === "creature"
  ? require('../assets/cards/creatures/' + props.name + '.jpg')
  : require('../assets/cards/equipment/' + props.name + '.jpg');
</script>

<template>
  <div class="card">
    <img class="card-image" :src="imgUrl">
    <p class="power">{{ props.power }}</p>
  </div>
</template>

<style scoped>
.card {
  margin: 2px;
  width: 10%;
  position: relative;
}

.power {
  position: absolute;
  top: .1vh;
  right: .5vw;
  font-weight: bold;
  color: black;
  font-size: calc(4px + 1vw);
}
</style>
